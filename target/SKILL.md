---
name: codepen
description: >
  Explore CodePen to find inspiration, evaluate interactive effects, and source production-ready code snippets for web builds. Use when the user says: 'find me a CodePen', 'search CodePen for', 'browse CodePen', 'find a pen for this effect', 'CodePen inspiration', 'look up CodePen examples', or asks to source code from CodePen for a specific UI pattern, animation, or interaction.
  Do NOT trigger for: building websites from scratch (use frontend-design), GSAP animation reference (use gsap-cheat-sheet-skills), 3D/WebGL development (use webgl-3d-dev), or general web design without CodePen sourcing (use web-coding-assistant).
---

# CodePen Exploration & Code Sourcing

Explore CodePen to discover what's possible — find inspiration, evaluate interactive effects, and source production-ready code snippets for website builds.

---

## Workflow

### Step 1: Search CodePen

Use `web_fetch` to search for relevant pens:

| Action | URL |
|--------|-----|
| Browse trending | `https://codepen.io/trending` |
| Search by keyword | `https://codepen.io/search/pens?q={search_term}` |
| Browse saved pens | `https://codepen.io/your-work` |

**Example search terms:** "GSAP scroll animation", "3D card hover", "text reveal animation", "parallax section", "liquid gradient background", "kinetic typography", "clip-path reveal"

Try multiple search terms — the first query rarely finds the best result.

### Step 2: Evaluate Pens

For each promising pen, assess:
- **Tech stack match**: Does it use vanilla JS or GSAP (preferred) vs. framework-specific code?
- **Code quality**: Is it clean, well-structured, and adaptable?
- **Dependencies**: What external libraries does it require?
- **Responsiveness**: Does it work on mobile?

### Step 3: Extract and Adapt

1. Fetch the individual pen page to extract HTML, CSS, and JavaScript
2. Document the pen's URL for attribution
3. Adapt the code to the project's design system, tech stack, and responsive requirements
4. Strip out unnecessary dependencies

### Step 4: Present Findings

Report to the user with:

```
## CodePen Research: [Topic]

### Pen 1: [Title]
- **URL**: [link]
- **What it does**: [brief description]
- **Tech**: [vanilla JS / GSAP / Three.js / etc.]
- **Adaptability**: [easy / moderate / needs significant rework]
- **Recommendation**: [use as-is / adapt / skip]

### Pen 2: [Title]
...

### Recommendation
[Which pen best fits the project and why]
```

---

## Design Process Integration

1. **Discovery**: Browse trending and search broadly before committing to a design direction — present options with links and descriptions
2. **Validation**: When a specific effect is proposed (e.g., "kinetic text hero"), search CodePen for working examples to assess feasibility
3. **Implementation**: Extract code from the selected pen and adapt it to the project

---

## Good vs Bad Example

User asks: "Find me a CodePen for a scroll-triggered text reveal effect."

❌ **Bad (lazy, no evaluation):**
> Here are some CodePen links about text animation. [dumps 5 URLs with no context]

✅ **Good (researched, evaluated, recommended):**
> ## CodePen Research: Scroll-Triggered Text Reveal
>
> ### Pen 1: "GSAP SplitText Scroll Reveal"
> - **URL**: [link from search]
> - **What it does**: Splits headline into characters, fades each in with staggered Y offset on ScrollTrigger
> - **Tech**: GSAP 3.12 + SplitText (Club plugin)
> - **Adaptability**: Easy — just update CSS variables for your font and colors
> - **Recommendation**: Best match — clean code, uses our primary animation library
>
> ### Pen 2: "CSS-Only Text Reveal"
> - **URL**: [link]
> - **What it does**: Pure CSS animation using clip-path on scroll (Intersection Observer)
> - **Tech**: Vanilla CSS + minimal JS
> - **Adaptability**: Easy but less flexible than GSAP approach
> - **Recommendation**: Good fallback if SplitText Club license isn't available
>
> ### Recommendation
> Go with Pen 1 — it uses GSAP (our standard) and the character-level control lets us fine-tune timing per word.

---

## Rules

- **Always attribute**: Document the pen URL when using code from CodePen
- **Prefer vanilla JS or GSAP** over framework-specific implementations
- **Document dependencies** before integrating any pen
- **Don't just dump links** — evaluate, compare, and recommend
