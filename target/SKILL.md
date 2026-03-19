---
name: figma-designer
description: >
  Transform Figma designs into production-ready, animated websites and components. Use this skill whenever the user mentions Figma, references a Figma file or URL, asks to extract designs from Figma, wants to convert Figma to code, or needs design tokens/variables pulled from Figma. Also trigger when the user says 'pull from Figma', 'match my Figma', 'Figma to HTML/React', 'design handoff', 'extract my design', or references design specs, component libraries, or design systems from Figma. Requires Figma MCP tools. Combines well with frontend-design and kinetic-minimalism skills.
  Do NOT trigger for: building websites without a Figma reference (use frontend-design or kinetic-minimalism), creating Figma diagrams in FigJam (use Figma MCP directly), 3D/WebGL development (use webgl-3d-dev), or general GSAP animation questions without a Figma design (use gsap-cheat-sheet-skills).
---

# Figma Designer Skill

Transform Figma designs into pixel-perfect, animated, production-grade websites and components. This skill orchestrates the full pipeline from Figma extraction to deployed code.

## Core Workflow

```
1. EXTRACT  →  Pull design context, variables, screenshots from Figma
2. ANALYZE  →  Map typography, colors, spacing, layout structure
3. PLAN     →  Decide animation strategy and component architecture
4. BUILD    →  Generate production code with animations
5. REFINE   →  Compare against screenshot, iterate
```

## Step 1: Extract from Figma

When the user references a Figma file or has one open in the Figma desktop app:

### Pull Design Context
Use `Figma:get_design_context` to extract UI code, layout specs, and component structure. If the user provides a Figma URL, extract the node ID from it:
- URL format: `https://figma.com/design/:fileKey/:fileName?node-id=1-2`
- Extracted nodeId: `1:2`

### Capture Visual Reference
Use `Figma:get_screenshot` to capture the exact visual appearance. This is your ground truth for pixel-perfect implementation.

### Map the Structure
Use `Figma:get_metadata` to get the full layer tree in XML format — node IDs, layer types, names, positions, and sizes. This helps understand the component hierarchy.

### Extract Design Tokens
Use `Figma:get_variable_defs` to pull the design system variables:
- Colors (primary, secondary, accent, neutrals)
- Typography scales (font families, sizes, weights, line heights)
- Spacing values (padding, margins, gaps)
- Border radius, shadows, and other tokens

### Check Code Connect
Use `Figma:get_code_connect_map` to see if components are already mapped to codebase components. This avoids rebuilding what already exists.

## Step 2: Analyze the Design

After extraction, build a **Design Brief** that captures:

### Typography System
```
Primary Font:     [extracted or identified from screenshot]
Secondary Font:   [if applicable]
Scale:            [h1 → body sizes, weights, letter-spacing]
Special:          [any display/decorative fonts]
```

### Color Palette
```
Background:       [hex + css variable name]
Text Primary:     [hex]
Text Secondary:   [hex]
Accent:           [hex]
Surface:          [hex for cards/containers]
Border:           [hex]
```

### Layout Grid
```
Max Width:        [container width]
Columns:          [grid system]
Gutter:           [gap between columns]
Breakpoints:      [responsive behavior]
```

### Component Inventory
List all unique components identified:
- Navigation (type: sticky/fixed/relative)
- Hero section (layout pattern)
- Cards/tiles (grid arrangement)
- CTAs (button styles)
- Footer structure

## Step 3: Plan Animation Strategy

Based on the design's aesthetic, select the appropriate animation approach.
Read `references/animation-patterns.md` for the full animation library.

### Animation Selection Matrix

| Design Aesthetic | Recommended Approach | Key Techniques |
|-----------------|---------------------|----------------|
| Institutional/Corporate | Subtle reveals | Fade-up on scroll, staggered text |
| Luxury/Premium | Kinetic minimalism | Parallax, smooth scroll, letter animations |
| Tech/SaaS | Dynamic interactions | Hover states, micro-animations, counters |
| Creative/Portfolio | Bold motion | Page transitions, 3D transforms, morphing |
| Editorial/Magazine | Typography-led | Text reveals, pull quotes, reading progress |

### Default Animation Stack
Unless the design suggests otherwise, implement:
1. **Page load**: Staggered fade-in of hero elements (0.6s, ease-out)
2. **Scroll reveals**: Elements animate in as they enter viewport
3. **Hover states**: Subtle scale/color transitions on interactive elements
4. **Navigation**: Smooth scroll with active state tracking

## Step 4: Build Production Code

### Technology Decisions

**Single-page / Landing page:**
- HTML + CSS + vanilla JS + GSAP (via CDN)
- Output as single `.html` artifact

**Multi-component / App:**
- React (`.jsx`) with Tailwind CSS
- GSAP via import or CDN

**WordPress integration:**
- Generate clean HTML/CSS that can be embedded
- Provide separate CSS file if needed

### Implementation Checklist

Before writing code, verify:
- [ ] All fonts loaded (Google Fonts CDN or system fonts)
- [ ] Color variables defined as CSS custom properties
- [ ] Responsive breakpoints planned (mobile-first)
- [ ] GSAP CDN included if animations needed
- [ ] ScrollTrigger plugin registered if scroll animations used
- [ ] Images referenced with proper paths or placeholders

### Code Quality Standards

**CSS Architecture:**
```css
:root {
  /* Colors extracted from Figma */
  --color-bg: #0a0a0a;
  --color-text: #ffffff;
  --color-accent: #c8a050;
  /* Typography */
  --font-display: 'Bank Gothic', sans-serif;
  --font-body: 'Inter', sans-serif;
  /* Spacing */
  --space-section: clamp(80px, 10vw, 160px);
}
```

**GSAP Initialization Pattern:**
```javascript
// Register plugins
gsap.registerPlugin(ScrollTrigger);

// Batch scroll reveals
gsap.utils.toArray('.reveal').forEach(el => {
  gsap.from(el, {
    y: 40,
    opacity: 0,
    duration: 0.8,
    ease: 'power2.out',
    scrollTrigger: {
      trigger: el,
      start: 'top 85%',
      toggleActions: 'play none none none'
    }
  });
});
```

**Responsive Pattern:**
```css
/* Mobile-first, then scale up */
.hero-title {
  font-size: clamp(2rem, 5vw, 4.5rem);
  line-height: 1.1;
}
```

## Step 5: Refine and Compare

After initial build:
1. Take a screenshot of the Figma design (`Figma:get_screenshot`)
2. Visually compare against your implementation
3. Check for:
   - Font matching (family, size, weight, spacing)
   - Color accuracy (compare hex values)
   - Spacing consistency (padding, margins)
   - Layout alignment (grid, flex behavior)
   - Responsive behavior at breakpoints
4. Iterate until the implementation matches the design

## Special Workflows

### Figma URL Extraction
When user pastes a Figma URL:
1. Parse the URL to extract `fileKey` and `node-id`
2. Convert `node-id` format: `1-2` in URL becomes `1:2` as nodeId
3. Use the nodeId with all Figma tools

### Design System Generation
When user asks to create design system rules:
1. Use `Figma:create_design_system_rules` to generate coding guidelines
2. Combine with extracted variables for a complete design system
3. Output as a reference document or CSS variables file

### Component Mapping
When user wants to connect Figma to existing code:
1. Use `Figma:get_code_connect_map` to see existing mappings
2. Use `Figma:add_code_connect_map` to create new mappings
3. Document the component library with Figma ↔ Code references

### Multi-Page Site from Figma
When the design has multiple pages/frames:
1. Use `Figma:get_metadata` on the page node to see all frames
2. Extract each frame individually with `Figma:get_design_context`
3. Identify shared components (nav, footer, typography)
4. Build shared CSS first, then page-specific layouts
5. Ensure consistent animations across pages

## Animation Reference

For detailed animation patterns, recipes, and GSAP configurations:
→ Read `references/animation-patterns.md`

This reference includes:
- 20+ scroll animation recipes
- Typography animation techniques
- Parallax implementation patterns
- Page transition effects
- Performance optimization tips

## Institutional Finance Aesthetic

For premium institutional websites (private equity, venture capital, advisory):
→ Read `references/institutional-finance.md`

This reference covers:
- Approved color palettes (abyssal blue, steel grey, etc.)
- Typography pairings (Bank Gothic, Novecento Sans Wide)
- Layout patterns from top PE/VC firms
- Animation restraint guidelines
- Trust-building design patterns

## Common Pitfalls

1. **Don't over-animate**: Institutional sites need restraint. 2-3 animation types max.
2. **Don't ignore mobile**: Always test responsive. GSAP ScrollTrigger needs `matchMedia` for mobile.
3. **Don't skip font loading**: Use `font-display: swap` and preload critical fonts.
4. **Don't hardcode colors**: Always use CSS variables extracted from Figma tokens.
5. **Don't forget performance**: Use `will-change` sparingly, prefer `transform` and `opacity` for animations.
6. **Don't rebuild mapped components**: Check Code Connect before building from scratch.
