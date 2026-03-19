---
name: workflow-to-manual-skill
description: >
  Transforms any described workflow into a step-by-step manual covering folders, files, prompts, MCPs, skills, and plugins needed to run it. Use when the user says: 'turn this into steps', 'make me a manual', 'how do I set this up', 'what do I need to do first', 'write setup instructions for this workflow', or describes a repeatable process they want to run using Claude Desktop, Cowork, or Claude Code.
  Do NOT trigger for: designing workflow architecture (use architecture), orchestrating self-improving agent loops (use workflow-orchestration), preparing a workflow definition file (use prepare-workflow), or executing a workflow directly (just do it — this skill only produces documentation).
---

Workflow-to-Manual Skill
Purpose
This skill transforms any described workflow into a clear, step-by-step manual that tells the user exactly what to set up on their computer — folders, files, prompts, MCPs, skills, and plugins — before they can run it. Every time the user describes a workflow, Claude produces a structured setup-and-execution guide.

When to Activate
Activate this skill whenever the user describes a workflow, automation, or repeatable process they want to run using Claude (Desktop, Cowork, Claude Code, Projects, or any combination). Also activate when the user says things like:

"How do I set this up?"
"Turn this into steps"
"Make me a manual for this"
"What do I need to do first?"
Or simply describes a desired outcome involving files, prompts, MCPs, or skills


Output Format
For every workflow described, produce a manual with these exact sections:

📋 WORKFLOW MANUAL: [Workflow Name]
One-line summary: [What this workflow does in plain English]

SECTION 1: PREREQUISITES — What You Need Before You Start
List every dependency. Be explicit. Assume the user has never done this before.
Software & Access:

 [e.g., Claude Desktop installed and logged in]
 [e.g., Claude Pro/Team subscription for Cowork access]
 [e.g., Chrome browser installed]

MCP Servers Required:

 [MCP name] — [what it does] — [how to install/enable it, or link to docs]
 [Repeat for each MCP]

Custom Skills Required:

 [Skill name] — [whether it needs to be created first or already exists]

Plugins Required:

 [Plugin name] — [official or custom, how to install]

If none are needed for a category, write "None required."

SECTION 2: FOLDER SETUP — What to Create on Your Computer
Provide the exact folder structure to create. Use a tree diagram.
Copy/[Root Folder Name]/
├── /[subfolder_1]/          ← [what goes here]
├── /[subfolder_2]/          ← [what goes here]
├── [filename.ext]           ← [what this file is / where to get it]
├── [filename.ext]           ← [what this file is / where to get it]
└── [filename.ext]           ← [what this file is / where to get it]
Step-by-step to create this:

Open Finder/File Explorer
Navigate to [location, e.g., Desktop or Documents]
Create a new folder called [name]
Inside that folder, create subfolders: [list]
Place the following files into the root folder: [list each file and where it comes from]
Place the following files into [subfolder]: [list]


SECTION 3: FILES TO PREPARE — What Goes in Each Folder
For each file the workflow needs, specify:
FileFormatWhat It ContainsWhere to Get / Create ItWhich Folder[name][.xlsx/.pptx/.txt/.pdf/etc.][description][create manually / export from X / download from Y]/[folder]
If a file needs specific structure (like a spreadsheet with certain columns), describe it:

[filename.ext] structure:

Column A: [label] — [description]
Column B: [label] — [description]
[etc.]



SECTION 4: CLAUDE SETUP — Where to Configure Things
Depending on the workflow, walk through the exact Claude interface steps:
If using Claude Projects (Chat):

Open Claude Desktop → Chat
Click "Projects" → "New Project"
Name it: [name]
In Project Instructions, paste the following:

Copy[Exact project instructions text]

Upload these files to the project: [list]

If using Cowork:

Open Claude Desktop → Cowork
Click "Choose folder" → select /[folder path]
[If importing from a Project]: Go to your [Project Name] project → click "Add to Cowork"
In the Cowork text box, paste the prompt from Section 5

If using Claude Code:

Open Claude Code
Navigate to /[folder path]
Paste the prompt from Section 5

MCP Configuration:

In Claude Desktop → Settings → MCP Servers (or Cowork → Settings → Capabilities)
Ensure the following are toggled ON:

 [MCP name]
 [MCP name]



Skills Configuration:

[If skill needs to be created first, say so and point to a creation step]
In Cowork → Settings → Capabilities → Add Skill
Upload [skill file/ZIP]
Verify by prompting: "List all skills you can access"

Plugins Configuration:

In Cowork → Add Plugin → [Upload / Choose from official list]
Install [plugin name]
Verify by prompting: "List all commands and skills in the [plugin name] plugin"


SECTION 5: THE PROMPT(S) — Exactly What to Paste
Provide every prompt the user needs to copy-paste, in execution order.
Prompt 1 of [N] — [Purpose, e.g., "Run the main workflow"]
Where to paste this: [Cowork text box / Claude Code / Chat project]
Copy[Exact prompt text, fully written out, ready to copy-paste. Include all specifics — file names, folder references, MCP tool names, skill names, output file names, parallel task instructions, progress tracker requests, etc.]
Prompt 2 of [N] — [Purpose, e.g., "Verification / follow-up"]
Where to paste this: [location]
Copy[Exact prompt text]
[Repeat for each prompt in the stack]

SECTION 6: WHAT TO EXPECT — Outputs & Where to Find Them
OutputFormatWhere It Will Be SavedWhat It Contains[name][.pptx/.xlsx/.html/etc.]/[folder]/[filename][description]
During execution, you should see:

 [e.g., A to-do list appearing in Cowork showing sub-tasks]
 [e.g., Sub-agents spinning up for parallel tasks]
 [e.g., Progress tracker updating as files are processed]
 [e.g., Files appearing in your output folder as they're generated]


SECTION 7: TROUBLESHOOTING & VERIFICATION
After the workflow completes, verify:

 [Check: e.g., Open the spreadsheet and confirm all rows have status "Complete"]
 [Check: e.g., Count output files in /ad_creatives — should be [N] images]
 [Check: e.g., Open the deck and confirm it follows the brand template]

If something went wrong:

Missing outputs? → Paste this follow-up prompt: "Double-check the progress tracker and confirm no [items] were skipped. If any are missing, process them and update the outputs."
MCP not working? → Go to Settings → MCP Servers → confirm [name] shows a green status. Restart Claude Desktop if needed.
Skill not recognized? → Run: "List all skills you can access" and verify [skill name] appears.
Files not found? → Confirm the working folder in Cowork points to the correct path. Files must be in the root or specified subfolders.


SECTION 8: MAKING IT REUSABLE (Optional)
If the user wants to reuse this workflow:
To run this again with new inputs:

[e.g., Replace the transcript file in /[folder] with the new one]
[e.g., Update row data in the master spreadsheet]
[e.g., Re-run Prompt 1 from Section 5]

To package this as a skill:
Paste this prompt in Claude Code pointing to your skill library folder:
Copy[Provide the exact skill-creation prompt tailored to this workflow]
To package this as a plugin (for team sharing):
Paste this prompt in Claude Code:
Copy[Provide the exact plugin-creation prompt if applicable]

Processing Rules
When generating a manual, follow these rules:

Never assume the user knows where to click. Spell out the interface path (e.g., "Claude Desktop → Cowork → Settings → Capabilities").
Always provide copy-paste-ready prompts. Never say "write a prompt that does X." Write the actual prompt.
Always specify exact file names and folder paths. Use the names from the user's description, or propose sensible defaults and flag them as suggestions.
If the workflow requires an MCP, state which one and how to enable it. If you don't know the exact installation steps, say: "Ensure [MCP name] is installed and enabled — check Claude's MCP documentation for setup instructions."
If the workflow involves skills that don't exist yet, include a creation step BEFORE the execution step. Make it clear the user must build the skill first.
If the workflow involves parallel sub-tasks, explicitly note this in the prompt and in the "What to Expect" section.
If information is missing from the user's description, ASK before generating. Specifically ask about:

What files they already have vs. need to create
Which MCPs they have installed
Whether they want outputs in specific formats
Whether this should be a one-off or reusable (skill/plugin)


Scale the manual to the complexity. A simple one-prompt workflow gets a shorter manual. A multi-MCP, multi-skill pipeline gets the full treatment with all 8 sections.
Use checkboxes for every action item so the user can track progress.
End every manual with the verification steps. Never skip Section 7.


Good vs Bad Example

User says: "I want to take a call transcript and turn it into a strategy deck using my brand template."

❌ **Bad (vague, no paths, no copy-paste prompt):**
> You'll need to set up a folder and upload your files. Then use Claude to process the transcript and create a deck. Make sure you have the right MCP servers enabled.

✅ **Good (specific, actionable, copy-paste ready):**
> **SECTION 2: FOLDER SETUP**
> ```
> ~/Documents/transcript-to-deck/
> ├── /input/              ← place your call transcript here (.txt or .pdf)
> ├── /templates/           ← place your brand PowerPoint template here (.pptx)
> └── /output/              ← Claude will save the finished deck here
> ```
>
> **SECTION 5: THE PROMPT**
> Prompt 1 of 1 — "Generate strategy deck from transcript"
> Where to paste: Cowork text box (with folder set to ~/Documents/transcript-to-deck/)
> ```
> Read the call transcript in /input/. Extract the key strategic themes, decisions, and action items. Then create a PowerPoint deck using the brand template in /templates/. Save the output to /output/strategy-deck-[date].pptx. Use the /michels-presentation-designer skill for slide design.
> ```

When this skill is triggered, produce the manual in this format. Scale to the complexity of the workflow described.