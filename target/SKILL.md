---
name: prepare-workflow
description: >
  Prepares a Claude workflow for execution by creating the folder structure, files, prompt stack, and MCP/skill configuration on the user's computer. Use when the user says: 'prepare this workflow', 'set up this workflow', 'get this workflow ready to run', 'create the folder and files for this', 'prepare the prompt stack', or describes a workflow they want scaffolded on their machine before running it.
  Do NOT trigger for: documenting a workflow as a manual (use workflow-to-manual-skill), designing workflow architecture (use architecture), orchestrating self-improving agent loops (use workflow-orchestration), or executing the workflow itself (just run it).
---

# Prepare Workflow

Set up everything a Claude workflow needs to run: folders, files, prompt stack, MCP servers, and skill configuration — so the user can execute with a single prompt.

---

## Process

### Step 1: Understand the Workflow

Ask the user (if not already clear):
1. **What does this workflow do?** (e.g., "turns call transcripts into strategy decks")
2. **What inputs are needed?** (files, URLs, data sources)
3. **What outputs should it produce?** (decks, spreadsheets, reports, images)
4. **Which Claude environment?** (Claude Desktop Chat/Projects, Cowork, Claude Code)
5. **Any MCP servers or skills required?** (e.g., Nano Banana for image generation, Chrome MCP for browsing)

### Step 2: Create the Folder Structure

Create the working folder with all necessary subfolders:

```bash
mkdir -p ~/Documents/[workflow-name]/{input,output,templates}
```

Organize by function:
- `/input/` — raw materials the workflow reads
- `/output/` — where generated files are saved
- `/templates/` — brand templates, guidelines, reference docs

### Step 3: Place or Create Required Files

For each file the workflow needs:
1. **If the user has it** → tell them exactly where to place it (e.g., "Put your brand template in `/templates/brand-template.pptx`")
2. **If it needs to be created** → create it (e.g., a master tracking spreadsheet with the right columns)
3. **If it's a config file** → generate it with the correct structure

### Step 4: Configure MCP Servers

For each required MCP server:
1. Check if it's already installed: have the user verify in Claude Desktop → Settings → MCP Servers
2. If not installed, provide setup instructions or link to docs
3. Confirm it shows green/active status

### Step 5: Configure Skills

For each required skill:
1. Check if it exists in the user's skill library
2. If it needs to be created first, create it before proceeding
3. Verify with: "List all skills you can access"

### Step 6: Write the Prompt Stack

Create the exact prompts the user will paste, in execution order. Each prompt must be:
- **Complete** — includes all file paths, folder references, MCP tool names, skill names
- **Copy-paste ready** — no placeholders the user needs to fill in (use the actual paths from Steps 2-3)
- **Explicit about parallelism** — if sub-tasks can run in parallel, say so

### Step 7: Verify Setup

Before the user runs anything, confirm:
- [ ] Folder structure exists with all required files in place
- [ ] MCP servers are installed and active
- [ ] Skills are accessible
- [ ] Prompt stack is ready to paste

---

## Output Format

When preparing a workflow, produce this structure:

```
## Workflow: [Name]
**Summary**: [One line — what this workflow does]
**Environment**: [Cowork / Claude Code / Chat Projects]

### Folder Structure
[Tree diagram with annotations]

### Files Placed
| File | Location | Source |
|------|----------|--------|
| [name] | /[path] | [user provides / auto-generated / template] |

### MCP Servers
| Server | Status | Setup |
|--------|--------|-------|
| [name] | [installed/needed] | [instructions if needed] |

### Skills Required
| Skill | Status |
|-------|--------|
| [name] | [available/needs creation] |

### Prompt Stack
**Prompt 1 of N** — [Purpose]
Where to paste: [location]
```
[exact prompt text]
```

### Ready to Run
[Checklist of verification items]
```

---

## Good vs Bad Example

User says: "Prepare a workflow that takes podcast transcripts and creates a growth strategy deck."

❌ **Bad (vague, no actual setup):**
> You'll need a folder with your transcripts and a prompt. Make sure you have the right tools.

✅ **Good (actually creates everything):**
> ```bash
> mkdir -p ~/Documents/growth-research/{transcripts,brand-docs,output}
> ```
>
> **Files to place:**
> | File | Location | Source |
> |------|----------|--------|
> | *.txt transcripts | /transcripts/ | User provides |
> | brand-guidelines.pdf | /brand-docs/ | User provides |
>
> **Prompt 1 of 1** — "Analyze transcripts and create strategy deck"
> Where to paste: Cowork text box (folder: ~/Documents/growth-research/)
> ```
> Read all podcast transcripts in /transcripts/ and the brand context in /brand-docs/. Create a progress tracker to tick off each transcript. Then: (1) Extract top growth frameworks, tools, and themes into a spreadsheet. (2) Create a growth strategy deck for our brand using the most relevant frameworks, with implementation steps and metrics. Save all outputs to /output/. If any transcripts were missed, re-scan and update.
> ```

---

## Rules

- **Actually create the folders and files** — don't just describe them. Use bash commands to set up the structure.
- **Never use placeholders in prompts** — use the real paths and file names from the setup steps.
- **Ask before assuming** — if you don't know what MCP servers the user has, ask.
- **Scale to complexity** — a simple single-prompt workflow gets a lean setup. A multi-MCP pipeline with parallel tasks gets the full treatment.
- **Test the setup** — after creating folders and files, verify they exist before handing off the prompt stack.
