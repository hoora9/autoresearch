---
name: notebooklm
description: Google NotebookLM integration via MCP server + Python API for research, content generation, and automation.
---



Interact with Google NotebookLM using two complementary tools:

- **`nlm`** (notebooklm-mcp-cli) — CLI + MCP server for real-time AI-assisted interaction (29 tools)
- **`notebooklm`** (notebooklm-py) — CLI + async Python API for batch automation and advanced scripting

## When to Use Which

| Use Case | Tool |
|---|---|
| Quick interactive commands via natural language | `nlm` (MCP) |
| Creating/listing/querying notebooks | Either |
| Generating audio, video, slides, quizzes | Either |
| Batch downloads, export in multiple formats | `notebooklm` (Python API) |
| Complex multi-step automation pipelines | `notebooklm` (Python API) |
| Sharing & collaboration management | `nlm` |
| Web/Drive research with auto-import | `nlm` |
| Slide revision with natural language | `notebooklm` |
| Mind map JSON extraction | `notebooklm` |

## Setup

### First-time Installation

Run the setup script:
```bash
bash ~/.agents/skills/notebooklm/scripts/setup.sh
```

### Authentication (Required)

Both tools need separate authentication via browser login:

```bash
# Authenticate notebooklm-mcp-cli
nlm login

# Authenticate notebooklm-py
notebooklm login
```

### MCP Server Setup

Configure the MCP server for your AI assistant:
```bash
nlm setup add antigravity   # For Antigravity
nlm setup add claude-code   # For Claude Code
nlm setup add cursor        # For Cursor
nlm setup add gemini        # For Gemini CLI
```

> **Note:** The MCP server exposes 29 tools. Disable it when not using NotebookLM to save context window.

## CLI Quick Reference

### `nlm` — Interactive Commands

```bash
nlm notebook list                          # List all notebooks
nlm notebook create "Research Project"     # Create notebook
nlm source add <notebook> --url "URL"      # Add URL source
nlm notebook query <notebook> "question"   # Ask a question
nlm audio create <notebook> --confirm      # Generate podcast
nlm download audio <notebook> <id>         # Download audio
nlm share public <notebook>                # Enable public link
nlm research start "topic" --max-sources 10  # Web research + auto-import
nlm doctor                                 # Diagnose issues
nlm --ai                                   # AI-consumable docs
```

### `notebooklm` — Python-Powered CLI

```bash
notebooklm login                           # Authenticate
notebooklm create "My Research"            # Create notebook
notebooklm use <notebook_id>               # Set active notebook
notebooklm source add "https://..."        # Add URL source
notebooklm source add "./paper.pdf"        # Add local file
notebooklm ask "What are the key themes?"  # Chat with sources
notebooklm generate audio "make it fun" --wait   # Generate podcast
notebooklm generate video --style whiteboard     # Generate video
notebooklm generate quiz --difficulty hard        # Generate quiz
notebooklm generate flashcards --quantity more    # Flashcards
notebooklm generate slide-deck                    # Slide deck
notebooklm generate mind-map                      # Mind map
notebooklm download audio ./podcast.mp3           # Download audio
notebooklm download quiz --format json ./quiz.json  # Download quiz as JSON
notebooklm download mind-map ./mindmap.json       # Download mind map
```

## Python API (Advanced Automation)

For complex workflows, use the async Python API directly:

```python
import asyncio
from notebooklm import NotebookLMClient

async def main():
    async with await NotebookLMClient.from_storage() as client:
        # Create notebook and add sources
        nb = await client.notebooks.create("Research")
        await client.sources.add_url(nb.id, "https://example.com", wait=True)

        # Chat with your sources
        result = await client.chat.ask(nb.id, "Summarize this")
        print(result.answer)

        # Generate and download content
        status = await client.artifacts.generate_audio(nb.id, instructions="engaging")
        await client.artifacts.wait_for_completion(nb.id, status.task_id)
        await client.artifacts.download_audio(nb.id, "podcast.mp3")

        # Generate quiz and export as JSON
        status = await client.artifacts.generate_quiz(nb.id)
        await client.artifacts.wait_for_completion(nb.id, status.task_id)
        await client.artifacts.download_quiz(nb.id, "quiz.json", output_format="json")

asyncio.run(main())
```

Run scripts with: `python3 ~/.agents/skills/notebooklm/scripts/batch_workflow.py`

## Batch Workflow Script

An example batch script is included at `scripts/batch_workflow.py`. It demonstrates:
- Creating a notebook from multiple URLs
- Generating an audio overview + quiz
- Downloading all artifacts locally

Usage:
```bash
python3 ~/.agents/skills/notebooklm/scripts/batch_workflow.py \
  "My Research Topic" \
  "https://url1.com" "https://url2.com" \
  --output-dir ./output
```

## Important Notes

- Both tools use **undocumented Google APIs** — they may break if Google changes endpoints
- Use a **dedicated Google account** if concerned about TOS
- Cookies expire periodically — re-run `nlm login` or `notebooklm login` if you get auth errors
- See `nlm doctor` for diagnostics if things aren't working
