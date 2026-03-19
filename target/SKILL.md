---
name: mcp-malicious-activity-checker
description: >
  Audit MCP (Model Context Protocol) servers for malicious code, prompt injections,
  and security vulnerabilities. Use this skill whenever a user asks to check, audit,
  review, or verify the safety of an MCP server, MCP tool, MCP integration, or any
  third-party server they're about to connect to Claude. Also trigger when a user
  mentions concerns about prompt injection, data exfiltration, supply chain attacks,
  or suspicious behavior in an MCP context. Even if the user just says "is this MCP
  safe?" or "check this repo for me" in the context of MCP servers, use this skill.
---

# MCP Malicious Activity Checker

A security auditing guide for inspecting MCP servers before connecting them to Claude or any LLM.

## When to Use

- User wants to verify an MCP server is safe before installing
- User is concerned about prompt injection in MCP tool descriptions
- User wants to audit source code of an MCP integration
- User asks "is this MCP safe?" or "should I trust this server?"

## Audit Workflow

Follow these steps in order when auditing an MCP server.

### Step 1: Read the Source Code

If the repo is open source, inspect every file — especially the `src/` folder (or equivalent entry points). Clone or browse the repository and examine:

- The main server file (where tools are registered)
- All tool definition files
- Any middleware or helper modules
- Configuration files

### Step 2: Check for Red Flags

Scan the codebase for these specific threats:

**Hardcoded suspicious URLs**
Look for outbound URLs that aren't the expected API domains. If the MCP server is for Facebook/Instagram, the only legitimate domains are `graph.facebook.com` and `graph.instagram.com`. Any other destination for tokens or user data is a red flag.

**Obfuscated code**
Watch for base64-encoded strings, `eval()`, `exec()` calls, or dynamically constructed code that hides its true purpose.

**Hidden prompt injection strings**
Text buried in tool descriptions or response values designed to manipulate the LLM. Look for phrases like:
- "ignore previous instructions"
- "you are now..."
- "disregard"
- "system:" prefixes in tool output
- Any instruction-like text in fields that should only contain data

**Credential exfiltration**
Code that reads `.env` variables, tokens, API keys, or session data and sends them to an external endpoint.

**Unexpected network calls**
HTTP requests to domains unrelated to the server's stated purpose.

**Malicious post-install scripts**
Code in `setup.py`, `postinstall` hooks, or similar that runs automatically after package installation.

### Step 3: Run Practical Checks

Execute these commands after cloning the repository:

**Search for dangerous function calls (Python):**
```bash
grep -r "eval\|exec\|subprocess\|os.system" src/
```

**Search for prompt injection patterns:**
```bash
grep -ri "ignore.*instruction\|system.*prompt\|disregard\|you are now\|forget.*previous" src/
```

**Check dependencies for known packages:**
Review `requirements.txt` or `package.json` — verify all dependencies are well-known, legitimate packages. Watch for typo-squatting (e.g., `reqeusts` instead of `requests`).

**Run a Python security linter (if Python):**
```bash
pip install bandit && bandit -r src/
```

**Run Semgrep for broader pattern detection:**
```bash
pip install semgrep && semgrep --config=auto src/
```

**For Node.js MCP servers:**
```bash
grep -r "eval\|Function(\|child_process\|exec\|spawn" src/
npm audit
```

### Step 4: Assess Repository Trust Signals

Check these indicators on GitHub (or equivalent):

- **Stars and forks** — Higher numbers suggest community trust, but aren't guarantees
- **Number of contributors** — Multiple contributors means more eyes on the code
- **License** — MIT, Apache 2.0, etc. are standard; no license or unusual licenses are a yellow flag
- **Issue tracker** — Check for reports of suspicious behavior
- **Commit history** — Look for recent large commits that could introduce malicious code
- **Organization vs. personal repo** — Org-backed repos often have more oversight

### Step 5: Summarize Findings

Present a clear security report with:

1. **Overall risk assessment** (Low / Medium / High / Critical)
2. **Findings** — Each red flag discovered, with file paths and line numbers
3. **Trust signals** — Positive indicators from the repository
4. **Recommendation** — Whether to proceed, proceed with caution, or avoid

## Example Output Format

```
## MCP Security Audit: [Server Name]

**Risk Level:** Low ✅

### Findings
- No obfuscated code detected
- All network calls target expected API domains
- No prompt injection patterns found in tool descriptions
- Dependencies are all well-known packages

### Trust Signals
- 71 stars, 16 forks, 7 contributors
- MIT license
- Active maintenance (last commit 3 days ago)

### Recommendation
Safe to use. No malicious patterns detected.
```
