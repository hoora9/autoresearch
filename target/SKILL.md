---
name: notion-research-documentation
description: >
  Searches across your Notion workspace, synthesizes findings from multiple pages, and
  creates comprehensive research documentation saved as new Notion pages. Use this skill
  when the user says "research X in Notion", "find everything about X", "compile a report
  on X", "what do we know about X", "gather info on X from Notion", "create a research doc",
  "synthesize our notes on X", or asks to search Notion and produce structured documentation.
  Do NOT trigger for: meeting preparation (use notion-meeting-intelligence), capturing
  conversation insights (use notion-knowledge-capture), or turning specs into tasks
  (use notion-spec-to-implementation).
---

# Research & Documentation

Enables comprehensive research workflows: search for information across your Notion workspace, fetch and analyze relevant pages, synthesize findings, and create well-structured documentation.

## Quick Start

When asked to research and document a topic:

1. **Search for relevant content**: Use `Notion:notion-search` to find pages
2. **Fetch detailed information**: Use `Notion:notion-fetch` to read full page content
3. **Synthesize findings**: Analyze and combine information from multiple sources
4. **Create structured output**: Use `Notion:notion-create-pages` to write documentation

## Research Workflow

### Step 1: Search for relevant information

```
Use Notion:notion-search with the research topic
Filter by teamspace if scope is known
Review search results to identify most relevant pages
```

### Step 2: Fetch page content

```
Use Notion:notion-fetch for each relevant page URL
Collect content from all relevant sources
Note key findings, quotes, and data points
```

### Step 3: Synthesize findings

Analyze the collected information:
- Identify key themes and patterns
- Connect related concepts across sources
- Note gaps or conflicting information
- Organize findings logically

### Step 4: Create structured documentation

Use the appropriate documentation template (see [reference/format-selection-guide.md](reference/format-selection-guide.md)) to structure output:
- Clear title and executive summary
- Well-organized sections with headings
- Citations linking back to source pages
- Actionable conclusions or next steps

## Output Format Specs

Choose format based on the user's needs:

| Format | When to use | Length | Structure |
|---|---|---|---|
| Quick Brief | "Give me a summary", time-sensitive requests | 200–400 words | Title → 3-sentence executive summary → 3–5 key findings (1 sentence each) → sources list |
| Research Summary | Default for most research requests | 500–1000 words | Title → executive summary (1 paragraph) → findings organized by theme (3–5 sections) → gaps/questions → recommended next steps → sources |
| Comprehensive Report | "Deep dive", "full report", complex topics | 1000–2500 words | Title → executive summary → methodology → findings by theme (5+ sections with citations) → analysis → gaps → recommendations → appendix of sources |

**Citation format:** Use Notion page mentions inline: "According to [Project Brief](notion-mention), the target launch date is..." Every claim from Notion must link to its source page.

### Good/Bad Example: Research Finding

> ✅ "Three separate project pages ([Q4 Planning](mention), [Marketing Roadmap](mention), [CEO Update Dec 2025](mention)) confirm the target launch date is March 2026. However, the [Engineering Status](mention) page (last updated Feb 15) flags a 2-week delay risk on the API integration. No page addresses the contingency plan for this delay."

> ❌ "Based on the available information, the project seems to be on track with some potential challenges. The team should continue monitoring progress and address any issues as they arise."

## Best Practices

1. **Cast a wide net first**: Start with broad searches, then narrow down
2. **Cite sources**: Always link back to source pages using mentions
3. **Verify recency**: Check page last-edited dates for current information
4. **Cross-reference**: Validate findings across multiple sources
5. **Structure clearly**: Use headings, bullets, and formatting for readability

## Page Placement

By default, create research documents as standalone pages. If the user specifies:
- A parent page → use `page_id` parent
- A database → fetch the database first, then use appropriate `data_source_id`
- A teamspace → create in that context

## Advanced Features

**Search filtering**: See [reference/advanced-search.md](reference/advanced-search.md)
**Citation styles**: See [reference/citations.md](reference/citations.md)

## Common Issues

**"No results found"**: Try broader search terms or different teamspaces
**"Too many results"**: Add filters or search within specific pages
**"Can't access page"**: User may lack permissions, ask them to verify access

## Examples

See [examples/](examples/) for complete workflow demonstrations:
- [examples/market-research.md](examples/market-research.md) - Researching market trends
- [examples/technical-investigation.md](examples/technical-investigation.md) - Technical deep-dive
- [examples/competitor-analysis.md](examples/competitor-analysis.md) - Multi-source synthesis

