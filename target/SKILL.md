---
name: web-coding-assistant
description: >
  A creative web development advisory team with specialists in motion graphics, WebGL, GSAP, and interactive design, plus CodePen code sourcing. Use when the user says: 'consult the design team', 'what would Bruno Simon do', 'find me a CodePen for this effect', 'help me build an interactive website', 'creative web development', or asks for expert-level advice on combining animation, 3D, and design in web builds. This skill provides advisor personas to consult and a CodePen research workflow.
  Do NOT trigger for: general frontend UI without animation (use frontend-design), Figma-to-code (use figma-designer), pure 3D/WebGL learning (use webgl-3d-dev), scroll-driven kinetic sites (use kinetic-minimalism), or GSAP API reference (use gsap-cheat-sheet-skills).
---

# Design & Motion Advisory Board

A curated team of world-class advisors in motion graphics, WebGL, GSAP, and creative technology. Consult them when building interactive, animated websites.

---

## Advisors

### 1. Bruno Simon — Creative Developer & WebGL Educator
**Specialty:** Three.js, WebGL, Interactive 3D Web Experiences
**Consult for:** Three.js architecture, 3D web performance, shader development, pushing browser rendering limits
**Signature approach:** Full-scene interactive 3D (his portfolio site lets users drive a car around a 3D landscape). Prioritizes playful interaction over passive viewing.

### 2. Matt DesLauriers — Artist & Creative Coder
**Specialty:** Generative Art, WebGL, Creative Coding, Shaders
**Consult for:** Generative design systems, shader artistry, blending fine art with code, cinematic visual quality in the browser
**Signature approach:** Algorithmic beauty — using noise functions, particle systems, and WebAudio to create art-quality experiences.

### 3. Guillaume Combeaud — 3D Motion Designer & Director
**Specialty:** 3D Motion Design, AI-Driven Creativity, Brand Animation
**Consult for:** Brand-level motion strategy, commercial animation direction, integrating AI into motion workflows, cinematic 3D for marketing
**Signature approach:** 17+ years of commercial motion for Adidas, North Face, Fender, Coca-Cola. Thinks in terms of brand narrative, not just technical execution.

### 4. Active Theory — Creative Digital Experience Studio
**Specialty:** Immersive WebGL, Custom Frameworks, VR/AR Web
**Consult for:** Scaling WebGL for enterprise, custom rendering frameworks, cross-platform 3D delivery, production pipelines
**Signature approach:** Built experiences for Google, NASA, Spotify. Uses Hydra (proprietary framework) for immersive 3D across web, mobile, and VR.

### 5. Codrops / Tympanus — Creative Web Development Lab
**Specialty:** GSAP, Scroll Animations, WebGL Shaders, UI Animation Patterns
**Consult for:** GSAP best practices, scroll-driven WebGL techniques, cutting-edge animation patterns, staying current with creative web trends
**Signature approach:** Publishes state-of-the-art tutorials combining GSAP, Three.js, WebGL shaders, and Barba.js. The benchmark for creative web animation.

### Quick Reference

| Advisor | Consult For |
|---|---|
| **Bruno Simon** | Three.js architecture, 3D interactivity, WebGL performance |
| **Matt DesLauriers** | Generative art, shaders, creative coding philosophy |
| **Guillaume Combeaud** | Brand motion strategy, commercial 3D, AI workflows |
| **Active Theory** | Enterprise WebGL, custom frameworks, cross-platform delivery |
| **Codrops** | GSAP patterns, scroll animation, experimental techniques |

---

## CodePen Exploration & Code Sourcing

### When to Use CodePen
Before finalizing design decisions, explore CodePen to discover what's possible — find inspiration, evaluate interactive effects, and source production-ready code snippets.

### Workflow

1. **Explore trending**: Fetch `https://codepen.io/trending` to see current UI patterns and animations
2. **Search for specific effects**: Fetch `https://codepen.io/search/pens?q={search_term}` — try terms like "GSAP scroll animation", "3D card hover", "text reveal animation", "parallax section"
3. **Check saved pens**: Fetch `https://codepen.io/your-work` for previously saved pens
4. **Extract code**: Fetch the individual pen page to get HTML, CSS, and JavaScript. Document the URL for attribution.

### Integration Rules
- Prefer pens using vanilla JS or GSAP (primary animation library) over framework-specific implementations
- Document all dependencies before integrating
- Adapt extracted code to the project's design system, responsive requirements, and tech stack

---

## Process

1. **Understand the brief**: What is the website's purpose, audience, and desired feel?
2. **Consult advisors**: Based on the brief, identify which advisor's expertise applies (e.g., Bruno Simon for 3D interactivity, Codrops for scroll animations)
3. **Research on CodePen**: Search for relevant effects and patterns to validate feasibility
4. **Plan the build**: Define the animation strategy, component architecture, and technology stack
5. **Build**: Generate production code combining advisor-level techniques with CodePen-sourced patterns
6. **Refine**: Compare output against the brief, iterate on animation timing and visual polish

---

## Good vs Bad Example

User asks: "Build me an interactive hero section for a creative agency."

❌ **Bad (generic, no advisor thinking):**
> Here's a hero with a fade-in title and a gradient background.

✅ **Good (advisor-informed, CodePen-researched):**
> Taking Bruno Simon's approach to interactive 3D: a WebGL particle field that reacts to cursor movement, with Codrops-style staggered text reveals. Found a relevant CodePen (GSAP character-by-character reveal) and adapted it. The particles use Three.js with custom shaders for a depth-of-field blur effect. Typography uses PP Neue Montreal at 7vw, letter-spacing expands on scroll. Dark palette with a single warm accent on the CTA.
