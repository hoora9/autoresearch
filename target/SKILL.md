---
name: canva-designer
description: Master Canva design creation, management, and automation via the Canva MCP Server. Use this skill whenever the user mentions Canva, wants to create designs, generate social media graphics, autofill brand templates, export designs as PDF or images, search existing Canva designs, resize designs for multiple platforms, import files into Canva, manage Canva folders and assets, create presentations or docs in Canva, or wants to use Canva's AI design generation including morphing effects. Also trigger when the user says "make me a Canva design", "create a social post", "autofill my template", "export from Canva", "resize for Instagram/LinkedIn/Facebook", "generate a presentation", "morph transition", or references brand kits, Magic Design, or any Canva workflow. This skill covers the full Canva MCP tool suite from design generation to batch operations and advanced creative techniques. Do NOT trigger for: PowerPoint/PPTX presentations (use michels-presentation-designer), Excalidraw diagrams (use excalidraw-diagram), Figma design work (use figma-designer), or general graphic design theory without Canva-specific actions.
---

# Canva Designer Skill

Create, manage, search, export, and automate Canva designs using the Canva MCP Server. This skill covers the complete Canva MCP tool suite including AI design generation, template autofill, multi-platform resizing, morphing effects, and batch workflows.

## Canva MCP Tools Reference

The Canva MCP Server (connected at `https://mcp.canva.com/mcp`) provides these core tools:

| Tool | Purpose |
|------|---------|
| `generate-design` | Create new designs using AI prompts (Magic Design) |
| `search-designs` | Search existing designs — docs, presentations, videos, whiteboards |
| `get-design` | Get detailed metadata about a specific design |
| `get-design-pages` | List pages in multi-page designs |
| `export-design` | Export designs as PDF, PNG, JPG |
| `autofill-design` | Fill brand templates with dynamic content |
| `create-design` | Create designs with preset or custom dimensions |
| `import-design` | Import external files (PDFs, etc.) into Canva |
| `resize-design` | Resize existing designs for different platforms |
| `upload-asset` | Upload images/assets to Canva |
| `create-folder` | Organize designs into folders |
| `list-folder-items` | Browse folder contents |
| `move-item` | Move designs between folders |
| `create-comment` | Add review comments to designs |
| `reply-to-comment` | Reply to existing design comments |

Note: The Canva MCP tool list evolves. If a tool isn't recognized, try describing the action naturally — the MCP server may support it under a different name.

## Core Workflows

### 1. Generate a Design from Scratch

Use `generate-design` with a detailed prompt. The more specific you are, the better the output.

**Effective prompt structure:**
```
Design type + Purpose + Visual style + Key content + Dimensions
```

**Examples of strong prompts:**
- "Create a professional Instagram post for a tech startup launch. Use dark navy background with gold accents. Include the headline 'AI That Works For You' and a futuristic abstract graphic. 1080x1080."
- "Generate a LinkedIn banner for Ocean Peak Capital, a private equity firm. Minimal, institutional aesthetic with deep blue tones. Include the tagline 'Navigating Global Markets' in clean sans-serif typography. 1584x396."
- "Create a presentation deck for a quarterly investor update. 10 slides with a clean white background, navy text, and subtle geometric accents. Include placeholder charts and data tables."

**Good vs. bad prompts:**
> ✅ "Create a professional Instagram post (1080x1080) for Belveo outdoor furniture. Background: warm sunset terrace scene. Colors: #2C3E50 navy text, #E67E22 accent. Headline: 'Votre terrasse, votre territoire.' Subtitle: 'Mobilier outdoor premium.' Clean sans-serif typography, minimal layout."
> ❌ "Make a nice Instagram post for a furniture company."

**Tips for generation:**
- Specify exact dimensions when you know the platform
- Reference specific color hex values for brand consistency
- Mention typography style preferences (serif, sans-serif, display)
- Include the number of pages/slides for multi-page designs
- Design generation is async — you'll receive a job ID to track progress

### 2. Search and Discover Existing Designs

Use `search-designs` to find designs across your Canva account.

**Search strategies:**
- Search by name: "Find all designs named 'Q3 Report'"
- Search by type: "Show me all my presentations"
- Search by recency: "Find designs from this month"
- Search by content: "Find designs containing 'product launch'"

**Combining search with actions:**
```
1. Search for designs → get design IDs
2. Get design details → understand structure
3. Export, resize, or autofill → transform as needed
```

### 3. Autofill Brand Templates

Use `autofill-design` to populate brand templates with dynamic data. This is powerful for scaling branded content.

**Autofill workflow:**
1. Identify the brand template ID (search or get from Canva)
2. Prepare the data payload (text fields, images, chart data)
3. Call autofill with the template ID and data
4. Export the result

**Data types supported:**
- Text fields (headlines, body copy, dates, names)
- Images (swap placeholder images)
- Chart data (bar charts, pie charts, line graphs with labeled data)
- Tables (structured data)

**Example:**
```
Autofill the "Monthly Report" template with:
- Title: "February 2026 Performance Report"
- Subtitle: "Ocean Peak Capital"
- Chart data: Revenue Q1: $12.5M, Q2: $14.2M, Q3: $16.8M, Q4: $19.1M
- Hero image: [uploaded asset ID]
```

Note: Autofill and Brand Templates require Canva Enterprise plan.

### 4. Export Designs

Use `export-design` to download designs in various formats.

**Supported formats:**
- **PDF** — Best for documents, presentations, print materials
- **PNG** — Best for social media, web graphics (supports transparency)
- **JPG** — Best for photos, smaller file sizes

**Export is async:** You'll receive a job ID. Poll for completion, then get download URLs.

**Quality options:**
- Standard quality — Default, suitable for web
- Pro quality — Higher resolution (may fail if design contains unpaid premium elements)

**Batch export pattern:**
```
1. Search for designs in a folder
2. Loop through results
3. Export each as PDF
4. Collect download links
```

### 5. Resize for Multiple Platforms

Use `resize-design` to adapt a single design for different platform dimensions.

**Common resize targets:**

| Platform | Format | Dimensions |
|----------|--------|------------|
| Instagram Post | Square | 1080 × 1080 |
| Instagram Story | Vertical | 1080 × 1920 |
| Facebook Post | Landscape | 1200 × 630 |
| Facebook Cover | Wide | 820 × 312 |
| LinkedIn Post | Landscape | 1200 × 627 |
| LinkedIn Banner | Wide | 1584 × 396 |
| Twitter/X Post | Landscape | 1600 × 900 |
| YouTube Thumbnail | Landscape | 1280 × 720 |
| Pinterest Pin | Vertical | 1000 × 1500 |
| TikTok | Vertical | 1080 × 1920 |
| A4 Print | Portrait | 2480 × 3508 |
| US Letter | Portrait | 2550 × 3300 |
| Business Card | Landscape | 1050 × 600 |
| Presentation | Widescreen | 1920 × 1080 |

**Multi-platform campaign workflow:**
```
1. Generate or find the master design
2. Resize for Instagram (1080×1080)
3. Resize for LinkedIn (1200×627)
4. Resize for Facebook Cover (820×312)
5. Export all variants
6. Organize into campaign folder
```

Note: Resize requires a paid Canva plan.

### 6. Import External Files

Use `import-design` to bring external files into Canva.

**Supported imports:**
- PDF files (converted to editable Canva pages)
- Files from URLs (no upload needed)
- Existing designs from other tools

**Use case:** Import a client's PDF brand guidelines, then use elements from it to create new Canva designs.

## Advanced Creative Techniques

For detailed creative workflows including morphing, animations, and visual effects:
→ Read `references/creative-techniques.md`

This reference covers:
- Morphing transitions between slides
- Animation and motion effects
- Visual consistency techniques
- Brand kit integration
- Advanced typography and color strategies
- Photo editing and enhancement within Canva

## Campaign and Batch Workflows

For multi-design campaigns and automation patterns:
→ Read `references/campaign-workflows.md`

This reference covers:
- Social media campaign generation (multi-platform)
- Batch autofill from data sources
- Folder organization strategies
- Team collaboration via comments
- Content calendar workflows
- Brand consistency at scale

## Design Prompting Best Practices

### DO:
- Be specific about dimensions, colors, and typography
- Reference brand colors by hex code when possible
- Specify the number of pages/slides for multi-page designs
- Include the purpose/audience for better AI generation
- Use Canva's design type presets when available (Instagram Post, Presentation, etc.)
- Iterate: generate → review → refine prompt → regenerate

### DON'T:
- Use vague prompts like "make something nice"
- Forget to specify dimensions (defaults may not match your platform)
- Skip organizing into folders (makes future searches harder)
- Assume exported files are final without reviewing in Canva editor
- Ignore brand kit settings if they exist in the account

## Async Job Handling

Many Canva operations are asynchronous (design generation, export, import, autofill). The pattern is:

```
1. Initiate the job → receive a job ID
2. Poll for completion (the MCP server handles this)
3. Receive the result (design ID, download URLs, etc.)
```

Generation typically takes a few seconds to a minute depending on complexity. If a job seems stuck, wait and retry — Canva's AI generation queue may have latency.

## Plan-Specific Features

| Feature | Free | Pro/Teams | Enterprise |
|---------|------|-----------|------------|
| Generate designs | ✓ (limited) | ✓ | ✓ |
| Search designs | ✓ | ✓ | ✓ |
| Export | ✓ | ✓ | ✓ |
| Resize | ✗ | ✓ | ✓ |
| Autofill templates | ✗ | ✗ | ✓ |
| Brand templates | ✗ | ✗ | ✓ |
| Pro export quality | ✗ | ✓ | ✓ |

## Common Pitfalls

1. **"Pro quality export failed"** — The design contains unpaid premium elements. Switch to standard quality or replace premium elements.
2. **"Design not found"** — The design may predate the MCP connection. Only designs created or modified after connecting are reliably accessible.
3. **"Autofill not available"** — Requires Canva Enterprise with brand templates configured.
4. **Resize distortion** — Canva intelligently re-layouts, but complex designs may need manual adjustment in the editor afterward.
5. **Rate limits** — Design generation uses Canva's AI and may be subject to usage limits based on account type.
