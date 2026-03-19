---
name: notebooklm
description: >
  Google NotebookLM integration via MCP server + Python API for research notebooks, AI-generated podcasts, quizzes, flashcards, mind maps, video summaries, and slide decks from source material. Use when the user asks to create a NotebookLM notebook, generate a podcast or audio overview from documents, make a quiz or flashcards from sources, build a mind map, create a slide deck from research, query sources in NotebookLM, import URLs or files into NotebookLM, or automate NotebookLM workflows.
  Do NOT trigger for: general note-taking (use Notion skills), audio editing or music production, generic quiz generation without NotebookLM, or research documentation without NotebookLM (use notion-research-documentation).
---

# NotebookLM Integration

Interact with Google NotebookLM using two complementary tools:

- **`nlm`** (notebooklm-mcp-cli) — CLI + MCP server for real-time AI-assisted interaction (29 tools)
- **`notebooklm`** (notebooklm-py) — CLI + async Python API for batch automation and advanced scripting

## Process

### Step 1: Check authentication

Before any NotebookLM operation, verify the user is authenticated:
```bash
nlm notebook list  # If this fails, run: nlm login
```
If using the Python API: `notebooklm login`

### Step 2: Choose the right tool

| Scenario | Use | Why |
|---|---|---|
| Quick one-off commands (create notebook, add source, ask question) | `nlm` CLI or MCP tools | Faster, interactive |
| Generate audio/video/quiz/slides | Either | Both support generation |
| Batch operations (multiple notebooks, bulk downloads) | `notebooklm` Python API | Async, scriptable |
| Sharing & collaboration | `nlm` | Has sharing commands |
| Web/Drive research with auto-import | `nlm` | Has `research start` |
| Complex multi-step pipelines | `notebooklm` Python API | Programmable control flow |

### Step 3: Execute the workflow

**For single operations**, use CLI commands directly:
```bash
nlm notebook create "Project Name"
nlm source add <notebook_id> --url "https://..."
nlm notebook query <notebook_id> "What are the key findings?"
nlm audio create <notebook_id> --confirm
```

**For batch/automation**, use the Python API:
```python
import asyncio
from notebooklm import NotebookLMClient

async def main():
    async with await NotebookLMClient.from_storage() as client:
        nb = await client.notebooks.create("Research")
        await client.sources.add_url(nb.id, "https://example.com", wait=True)
        result = await client.chat.ask(nb.id, "Summarize this")
        print(result.answer)
        status = await client.artifacts.generate_audio(nb.id, instructions="engaging")
        await client.artifacts.wait_for_completion(nb.id, status.task_id)
        await client.artifacts.download_audio(nb.id, "podcast.mp3")

asyncio.run(main())
```

### Step 4: Handle artifacts

After generating content, always:
1. Wait for generation to complete (audio/video can take 1-3 minutes)
2. Download the artifact to a local path the user can access
3. Report what was generated and where it was saved

## CLI Quick Reference

### `nlm` commands
```bash
nlm notebook list                            # List all notebooks
nlm notebook create "Name"                   # Create notebook
nlm source add <nb> --url "URL"              # Add URL source
nlm notebook query <nb> "question"           # Query sources
nlm audio create <nb> --confirm              # Generate podcast
nlm download audio <nb> <id>                 # Download audio
nlm share public <nb>                        # Public link
nlm research start "topic" --max-sources 10  # Web research + auto-import
nlm doctor                                   # Diagnose issues
```

### `notebooklm` commands
```bash
notebooklm create "Name"                          # Create notebook
notebooklm use <notebook_id>                      # Set active notebook
notebooklm source add "https://..." | "./file.pdf"  # Add source
notebooklm ask "question"                          # Chat with sources
notebooklm generate audio "instructions" --wait    # Podcast
notebooklm generate video --style whiteboard       # Video
notebooklm generate quiz --difficulty hard         # Quiz
notebooklm generate flashcards --quantity more     # Flashcards
notebooklm generate slide-deck                     # Slides
notebooklm generate mind-map                       # Mind map
notebooklm download audio ./output.mp3             # Download
```

## Setup (first-time only)

```bash
bash ~/.agents/skills/notebooklm/scripts/setup.sh  # Install
nlm login                                           # Auth for nlm
notebooklm login                                    # Auth for Python API
nlm setup add claude-code                            # Configure MCP server
```

## Important constraints

- Both tools use **undocumented Google APIs** — may break if Google changes endpoints
- Recommend a **dedicated Google account** if concerned about TOS
- Cookies expire periodically — re-run login commands if auth errors occur
- MCP server exposes 29 tools — disable when not using NotebookLM to save context window
- `nlm doctor` diagnoses common issues

## Output quality example

User: "Create a NotebookLM notebook from these 3 articles and generate a podcast"

❌ Bad output:
"I'll create a notebook for you. Use `nlm notebook create` to make a notebook, then add sources with `nlm source add`, then generate audio with `nlm audio create`."

✅ Good output:
"Creating your notebook and adding all 3 sources:

```bash
nlm notebook create 'Article Research'
# → Created notebook abc123

nlm source add abc123 --url 'https://article1.com'
nlm source add abc123 --url 'https://article2.com'
nlm source add abc123 --url 'https://article3.com'
# → 3 sources added, processing...

nlm audio create abc123 --confirm
# → Audio generation started (typically takes 1-3 minutes)

nlm download audio abc123 latest ./podcast.mp3
# → Downloaded to ./podcast.mp3
```

Your podcast is saved at `./podcast.mp3`. NotebookLM creates a conversational two-host format that covers the key themes across all three articles."
