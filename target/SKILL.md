---
name: visual-workflow-builder
description: >
  Generates interactive visual workflow diagrams from plain text descriptions — like Make.com, but inside Claude.
  Produces two outputs: (1) an interactive builder artifact where nodes can be dragged, connected, and edited,
  and (2) a polished client-facing presenter with step descriptions, tool badges, and annotations.
  Use this skill whenever the user describes a workflow, automation, process, or sequence of steps and wants
  it visualised. Trigger when the user says things like: "build me a workflow diagram", "show this as a flow",
  "make a visual of my automation", "diagram this process", "client-ready workflow", "Make.com-style flow",
  "visual workflow", "show the steps visually", or whenever they describe a multi-step process and want
  something to show a client or team. Also trigger when the user wants to update or add nodes to an existing
  workflow diagram built with this skill.
  Do NOT trigger for: simple text-based architecture plans (use architecture), Excalidraw hand-drawn
  diagrams without interactive nodes (use excalidraw-diagram), step-by-step manual/checklist creation
  (use workflow-to-manual-skill or prepare-workflow), or Mermaid diagram generation.
---

# Visual Workflow Builder

Generates two React artifacts from a plain text workflow description:

1. **Interactive Builder** — draggable nodes, clickable port connections, zoom/pan, double-click to edit labels
2. **Client Presenter** — read-only, annotated, scroll-through, with tool badges and step descriptions

---

## Step 1 — Parse the Workflow

The user may describe their workflow in plain terms like:

```
RESEARCH → DRAFT → HUMAN REVIEWS → APPROVE → SCHEDULE → POST
```

Or as a paragraph, bullet list, or conversation. Your job is to extract the structure:

```
WORKFLOW_NAME: (e.g. "LinkedIn Post Automation")
NODES: list of steps, each with:
  - id, label (short, 2 lines max), type, tool (optional), description (1 sentence)
EDGES: connections between nodes, each with:
  - from → to, optional label (e.g. "Yes ✓", "No ✗", "retry")
```

### Mapping plain language to node types

| Plain term | Node type | Why |
|---|---|---|
| "Schedule", "Trigger", "Every week", "When X happens" | `trigger` | Initiates the flow |
| "Research", "Draft", "Generate", "Save", "Send", "Post" | `action` | A task being done |
| "Human reviews", "Approve?", "Check", "If X then Y" | `decision` | A branch point |
| "Filter", "Only if", "Condition", "Transform" | `filter` | A gate/condition |
| "Post", "Publish", "Deliver", "Done", "Result" | `output` | End of the flow |

### Example: parsing the LinkedIn workflow

Input: `RESEARCH → DRAFT → HUMAN REVIEWS → APPROVE → SCHEDULE → POST`

Parsed nodes:
```js
{ id:"n1", type:"trigger",  label:"Weekly\nSchedule",    tool:"Make.com" }
{ id:"n2", type:"action",   label:"Deep Research\nSkill", tool:"Claude"   }
{ id:"n3", type:"action",   label:"Draft LinkedIn\nPost", tool:"Claude"   }
{ id:"n4", type:"action",   label:"Save to\nNotion",      tool:"Notion"   }
{ id:"n5", type:"decision", label:"Approved?",            tool:null       }
{ id:"n6", type:"output",   label:"Post to\nLinkedIn",    tool:"LinkedIn" }
{ id:"n7", type:"filter",   label:"Revise Draft",         tool:null       }
```

Parsed edges:
```js
n1→n2, n2→n3, n3→n4, n4→n5
n5→n6 (label: "Yes ✓")
n5→n7 (label: "No ✗")
n7→n3 (label: "retry")
```

---

## Step 2 — Generate Artifacts

Generate **both** artifacts in sequence. Tell the user what you're building before each one.

### Artifact 1: Interactive Builder

Use the BUILDER template from `references/builder-template.md`.

Key customisations to make:
- Replace `INIT_NODES` with parsed nodes (set x/y positions in a sensible left-to-right or top-to-bottom layout)
- Replace `INIT_EDGES` with parsed edges
- Set `WORKFLOW_TITLE` to the workflow name
- Position nodes so the flow reads naturally (left to right for linear, branching below for decisions)

**Layout guide:**
- Start node: x=100, y=center
- Each subsequent step: x += 230
- Decision branches: main path continues right, alternate path goes y += 180
- Keep y between 150–450 for single-path flows

### Artifact 2: Client Presenter

Use the PRESENTER template from `references/presenter-template.md`.

Key customisations:
- `WORKFLOW_TITLE` and `WORKFLOW_SUBTITLE` (e.g. "7-step automation · Human-in-the-loop")
- `STEPS_DATA` array — one entry per node, with: icon, color, title, tool badge, description, duration (optional)
- Include a summary header: total steps, tools used, human touchpoints
- Flow diagram at top (simplified SVG), then scrollable step cards below

---

## Step 3 — Offer Next Steps

After generating both artifacts, offer:
- "Want me to **export this to Excalidraw** for a hand-drawn shareable version?"
- "Want me to **save this to Notion** as a workflow doc?"
- "Want to **add more steps** or adjust any node?"
- "Want the **skill file** packaged for reuse?"

---

## Edge Cases

- **2–3 nodes only:** Still generate both artifacts. Use a compact horizontal layout (x spacing = 200).
- **No tools specified:** Omit tool badges. Use generic icons (gear for action, diamond for decision).
- **Parallel paths:** If the user describes steps that happen simultaneously, stack them vertically at the same x position and connect from a single source node.
- **Updates to existing diagram:** When the user says "add a step" or "change X", modify only the affected nodes/edges. Re-render both artifacts with changes highlighted.
- **Very large workflows (15+ nodes):** Switch to top-to-bottom layout. Group related nodes into labeled swimlanes if the user describes different teams or systems.

---

## Reference Files

- `references/builder-template.md` — Full React code for the interactive builder
- `references/presenter-template.md` — Full React code for the client presenter

**Important:** Read the relevant template file before generating each artifact. These templates contain the full React component code that you customize with the parsed workflow data.
