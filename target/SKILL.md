---
name: ai-screenshot-organizer
description: "Scan the user's Mac Photos library for AI-related screenshots, organize them into a dedicated folder, extract information from each screenshot, and build a Word document with a clickable numbered table of contents, categorized sections, and researched explanations. This is a living document that updates incrementally on each run. Use this skill whenever the user mentions organizing AI screenshots, extracting info from screenshots into a document, building an AI knowledge base from photos, or wants to scan their photos for AI-related content. Also trigger when the user says 'update my AI doc', 'scan for new AI screenshots', 'organize my AI folder', or references this workflow in any way."
---

# AI Screenshot Organizer

Scan the user's Photos for AI-related screenshots, extract and categorize the information, and maintain a living Word document that serves as a personal AI knowledge base.

## Overview

This skill performs the following workflow:

1. **Discover screenshots** in the Mac Photos library
2. **Visually analyze** each screenshot to determine if it's AI-related
3. **Copy AI screenshots** into `~/Documents/AI/screenshots/`
4. **Extract information** from each screenshot (text, URLs, tool names, concepts)
5. **Categorize** the extracted information into logical groups
6. **Research** each item briefly (1 paragraph max) using web search to add context
7. **Create or update** a Word document with a clickable numbered index and category sections
8. **Save** the document to `~/Documents/AI/` and a second copy to `~/Desktop/`

The document is a **living document** — each run only processes new screenshots and appends to the existing data, then regenerates the full document.

---

## Step 0: Folder Access

You need access to the user's file system. Use `request_cowork_directory` to ask the user to select a folder that gives you access to their home directory (or at minimum, their Pictures and Documents folders). If you already have folder access, skip this.

---

## Step 1: Locate Screenshots

Mac Photos stores images in a library package. Use Spotlight metadata to find screenshots efficiently:

```bash
# Find all screenshots on the Mac using Spotlight metadata
mdfind "kMDItemIsScreenCapture == 1" > /tmp/all_screenshots.txt
wc -l /tmp/all_screenshots.txt
```

If `mdfind` returns nothing, fall back to searching common locations:

```bash
find ~/Desktop ~/Pictures ~/Downloads -name "Screenshot*.png" -o -name "Screen Shot*.png" 2>/dev/null
```

You can also use `osascript` to export from the Photos app if direct file access doesn't reach synced iPhone photos:

```bash
osascript -e '
tell application "Photos"
    set allPhotos to every media item whose filename contains "Screenshot"
    repeat with p in allPhotos
        export {p} to POSIX file "/tmp/photo_export/" with using originals
    end repeat
end tell'
```

---

## Step 2: Filter Out Already-Processed Screenshots

The skill tracks what's been processed in `~/Documents/AI/.processed_screenshots.json`. This is how the "living document" feature works — future runs skip screenshots that were already handled.

```bash
mkdir -p ~/Documents/AI/screenshots
```

If the tracking file doesn't exist yet, create it:

```json
{"processed": [], "categories": {}, "lastUpdated": ""}
```

Use Python to filter the screenshot list down to only new (unprocessed) ones:

```python
import json, os

tracking_path = os.path.expanduser("~/Documents/AI/.processed_screenshots.json")
with open(tracking_path) as f:
    tracking = json.load(f)

processed = set(tracking["processed"])

with open("/tmp/all_screenshots.txt") as f:
    all_ss = [line.strip() for line in f if line.strip()]

new_ss = [s for s in all_ss if s not in processed]
print(f"Found {len(new_ss)} new screenshots to analyze (out of {len(all_ss)} total)")
```

If there are zero new screenshots, tell the user their AI document is already up to date.

---

## Step 3: Visual Analysis — Is It AI-Related?

For each new screenshot, use the `Read` tool to visually examine it. The Read tool can display images, so you can look at the screenshot content directly.

**AI-related includes:**
- AI tools (ChatGPT, Claude, Midjourney, Stable Diffusion, DALL-E, Copilot, Gemini, Perplexity, Runway, etc.)
- AI-generated images or art
- Conversations with AI assistants
- AI product pages, pricing, features
- Machine learning tutorials, code, documentation
- AI news or social media posts about AI
- Prompt engineering tips
- AI tool settings or API dashboards

**Not AI-related:**
- Random app screenshots unrelated to AI
- General web browsing not about AI
- Regular photos of people, food, scenery
- System settings or notifications unrelated to AI

For each AI-related screenshot, extract:
- **Title**: A short descriptive name for the content
- **What's shown**: The key information visible in the screenshot
- **Any URLs or commands**: Websites, terminal commands, or links visible
- **Category**: Which category it belongs to (see Step 5)

Process in batches of 5-10 and give the user progress updates.

---

## Step 4: Copy AI Screenshots

Copy confirmed AI-related screenshots to the organized folder:

```bash
cp "/path/to/screenshot.png" ~/Documents/AI/screenshots/
```

Keep original filenames. If there's a collision, append a number.

---

## Step 5: Categorize

Group extracted information into categories. Use these defaults and create new ones as needed:

1. **AI Chatbots & Assistants** — ChatGPT, Claude, Gemini, Copilot conversations
2. **Image Generation** — Midjourney, DALL-E, Stable Diffusion tools
3. **Image Galleries & Libraries** — Collections of AI-generated images
4. **Video Generation** — Sora, Runway, Pika, AI video tools
5. **Audio & Music** — AI music, voice cloning, text-to-speech
6. **Coding & Development** — AI coding assistants, GitHub Copilot, Cursor
7. **Writing & Content** — AI writing tools, content generators
8. **Research & Search** — Perplexity, AI-powered search
9. **Prompts & Tips** — Prompt engineering, best practices
10. **AI News & Updates** — Product launches, industry news
11. **Pricing & Plans** — AI tool pricing, subscriptions
12. **Tutorials & Guides** — How-to content, learning resources
13. **APIs & Technical** — API docs, technical configurations
14. **Other AI Tools** — Anything not covered above

Only include categories that have entries. If screenshots reveal a new category, add it.

---

## Step 6: Research Each Item

For each extracted piece of information, use `WebSearch` to find brief context. The goal is to help the user understand why each item is useful.

Rules for research:
- **Maximum 1 paragraph** (3-5 sentences)
- Focus on practical value: What is this? Why is it useful? How would someone use it?
- Write in clear, accessible language
- Include the URL/website if visible in the screenshot
- If web search finds nothing useful, just describe what's in the screenshot

---

## Step 7: Create or Update the Word Document

Read the docx SKILL.md at `/sessions/sweet-intelligent-lovelace/mnt/.skills/skills/docx/SKILL.md` for detailed Word document creation best practices.

Use the `docx` npm package (`npm install -g docx` if needed) to create the document.

### Document Structure

```
TITLE AREA:
  "AI Knowledge Base"
  "Personal AI Reference Document"
  Last updated: [date]
  Total entries: [count]

TABLE OF CONTENTS:
  Clickable numbered index using TableOfContents with hyperlink: true
  1. AI Chatbots & Assistants
  2. Image Generation
  3. Image Galleries & Libraries
  ... (only categories with entries)

CATEGORY SECTIONS:
  Each section:
  - Numbered heading matching TOC (e.g., "1. AI Chatbots & Assistants")
  - Uses HeadingLevel.HEADING_1 (required for TOC linking)
  - For each item:
    - Item title (HeadingLevel.HEADING_2)
    - Source screenshot filename (italic, small, gray)
    - Extracted information
    - Research paragraph
    - URL link if available
    - Visual separator
```

### Key Technical Requirements

- **Page size**: US Letter (12240 x 15840 DXA)
- **Margins**: 1 inch all around (1440 DXA)
- **Font**: Arial throughout
- **TOC must use HeadingLevel**: Only `HeadingLevel.HEADING_1` and `HEADING_2` work with `TableOfContents`. Custom styles won't link.
- **Override built-in heading styles**: Use exact IDs "Heading1", "Heading2" with `outlineLevel` set (0 for H1, 1 for H2)
- **Numbered categories**: The heading text itself should include the number (e.g., "1. AI Chatbots & Assistants")
- **Validate after creation**: Run `python scripts/office/validate.py doc.docx` if available

### On Update Runs

When the tracking file already has data from previous runs:
1. Load existing tracking data
2. Add new entries from newly processed screenshots
3. Regenerate the entire Word document from the complete tracking data (simpler and more reliable than editing the existing .docx in place)
4. Save the updated tracking file
5. Save the document to both locations

This means every run produces a complete, fresh document that includes all entries (old and new).

---

## Step 8: Save to Both Locations

```bash
# Primary location — same folder as the screenshots
cp "AI Knowledge Base.docx" ~/Documents/AI/

# Second copy on the Desktop
cp "AI Knowledge Base.docx" ~/Desktop/
```

Update the tracking file:

```python
import json, os
from datetime import datetime

tracking_path = os.path.expanduser("~/Documents/AI/.processed_screenshots.json")
with open(tracking_path) as f:
    tracking = json.load(f)

# Add newly processed screenshot paths
tracking["processed"].extend(newly_processed_paths)

# Update categories with new entries
for cat_name, items in new_entries.items():
    if cat_name not in tracking["categories"]:
        tracking["categories"][cat_name] = []
    tracking["categories"][cat_name].extend(items)

tracking["lastUpdated"] = datetime.now().isoformat()

with open(tracking_path, "w") as f:
    json.dump(tracking, f, indent=2)
```

---

## Step 9: Report to the User

After completion, summarize:
- How many new screenshots were found and analyzed
- How many were AI-related vs. not
- What categories and entries were added (or updated)
- Where the document is saved (both locations)
- Remind them: "Run this skill again anytime to pick up new screenshots!"

---

## Important Behavior Notes

- **Be patient with large libraries.** Process in batches, give progress updates.
- **When in doubt, include it.** Borderline AI screenshots should be included — the user can always prune later.
- **Keep research concise.** One paragraph max. Quick context, not a deep dive.
- **Never delete old entries.** Only add. The tracking file is append-only for the "processed" list and category items.
- **Handle errors gracefully.** If a screenshot can't be read or search fails, note it and keep going.
- **The TOC must be clickable.** This is the user's main navigation. Use HeadingLevel styles.
- **Number every category.** "1. Category Name", "2. Category Name", etc. — these numbers are how the user references sections.
