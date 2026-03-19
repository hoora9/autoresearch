---
name: kinetic-minimalism
description: >
  A motion-first web design system that fuses restrained, elegant aesthetics with purposeful,
  scroll-driven animation. Use this skill whenever the user wants to build websites, landing pages,
  portfolios, or institutional pages that feature scroll-triggered animations, GSAP effects,
  kinetic typography, parallax scrolling, smooth scroll experiences, micro-interactions, or
  any combination of minimalist design with sophisticated motion. Also trigger when the user
  mentions "motion design", "scroll animation", "GSAP", "ScrollTrigger", "ScrollSmoother",
  "kinetic type", "parallax", "entrance animations", "reveal effects", "scrub animation",
  "pin sections", "luxury web aesthetic", "institutional website", or wants to add life and
  motion to a clean, minimal layout. If the user asks for a website that should feel "premium",
  "cinematic", "alive", or "sophisticated" — this is the skill to use.
---

# Kinetic Minimalism — Motion & Design System

A philosophy where **less content meets more motion**. Every pixel is intentional, every animation earns its place. The result: websites that breathe, respond, and feel alive — without clutter.

## Core Philosophy

Kinetic Minimalism lives at the intersection of two forces:

1. **Restraint** — Clean layouts, generous whitespace, limited palettes, typographic hierarchy
2. **Intentional Motion** — Every animation has a narrative purpose: to guide, reveal, emphasize, or delight

The rule: **If it moves, it must mean something.** Decorative animation is noise. Purposeful animation is language.

---

## Design Principles

### The Five Laws of Kinetic Minimalism

1. **Motion as Hierarchy** — Animation defines what the eye sees first, second, third. Stagger reveals to create reading order.
2. **Whitespace is a Stage** — Empty space isn't wasted; it's where motion performs. Give animations room to breathe.
3. **One Hero Moment Per Viewport** — Each scroll-stop has ONE dominant animation. Supporting elements enter quietly.
4. **Easing is Emotion** — `power2.out` feels confident. `power4.out` feels dramatic. `back.out(1.2)` feels playful. Choose easing like you choose words.
5. **Performance is Design** — A janky animation is worse than no animation. 60fps or remove it.

### Visual Identity Parameters

When building a Kinetic Minimalism site, establish these tokens early:

| Token | Purpose | Recommended Range |
|-------|---------|-------------------|
| `--km-duration-fast` | Micro-interactions, hovers | `0.25s – 0.4s` |
| `--km-duration-medium` | Entrance reveals, transitions | `0.6s – 1.0s` |
| `--km-duration-slow` | Hero animations, scroll sequences | `1.2s – 2.0s` |
| `--km-stagger` | Delay between sequential reveals | `0.08s – 0.15s` |
| `--km-ease-default` | General motion | `power2.out` |
| `--km-ease-dramatic` | Hero moments | `power3.out` or `power4.out` |
| `--km-ease-smooth` | Scroll-scrubbed motion | `none` (linear for scrub) |
| `--km-translate-y` | Vertical entrance offset | `30px – 60px` |
| `--km-translate-x` | Horizontal entrance offset | `40px – 80px` |

---

## Typography in Motion

### Kinetic Typography Patterns

Kinetic type is the signature of this system. Text isn't static — it arrives, transforms, and responds.

**Pattern 1: Staggered Character Reveal**
Split headlines into individual characters. Reveal them sequentially with slight vertical offset and opacity fade. Use `SplitText` or manual `<span>` wrapping.

```js
// GSAP SplitText approach
const split = new SplitText(".hero-title", { type: "chars" });
gsap.from(split.chars, {
  y: 40,
  opacity: 0,
  duration: 0.6,
  stagger: 0.03,
  ease: "power3.out",
});
```

**Pattern 2: Line-by-Line Scroll Reveal**
Split paragraphs into lines. Tie each line's opacity and position to scroll progress via `scrub`.

**Pattern 3: Kinetic Headline on Scroll**
Pin a headline and transform it as the user scrolls — scale, rotate, color shift, or letter-spacing expansion.

**Pattern 4: Split-and-Part**
A word splits into two halves that slide apart, revealing an image or section beneath. Great for hero transitions.

### Font Selection Guidelines

Kinetic Minimalism demands typography that commands space:

- **Display / Headlines**: Choose fonts with strong geometry and presence. Bank Gothic, Novecento Sans Wide, PP Neue Montreal, Syne, Instrument Serif, Playfair Display, or custom variable fonts.
- **Body**: Clean, highly legible sans-serifs. Outfit, Satoshi, General Sans, DM Sans, or Switzer.
- **Monospace accents** (for labels, captions): JetBrains Mono, IBM Plex Mono, Fira Code.

NEVER default to Inter, Roboto, or Arial. These are invisible fonts — they have no kinetic presence.

---

## Color & Atmosphere

### Palette Construction

Kinetic Minimalism typically operates in one of three modes:

**Mode 1: Dark Institutional**
Deep backgrounds (near-black, navy, charcoal) with light text and a single accent color. Premium, authoritative.
```css
:root {
  --km-bg: #0a0a0f;
  --km-surface: #14141c;
  --km-text: #f0ece4;
  --km-muted: #6b6b7b;
  --km-accent: #c9a96e; /* warm gold */
}
```

**Mode 2: Light Editorial**
White/cream backgrounds, dark type, generous whitespace. The motion itself creates visual richness.
```css
:root {
  --km-bg: #faf9f6;
  --km-surface: #ffffff;
  --km-text: #1a1a2e;
  --km-muted: #9e9e9e;
  --km-accent: #2d5016; /* forest green */
}
```

**Mode 3: Tonal Monochrome**
Single-hue palette with value variations. Sophisticated and cohesive. Motion and type do all the heavy lifting.
```css
:root {
  --km-bg: #1a1a2e;
  --km-surface: #22223a;
  --km-text: #e8e8f0;
  --km-muted: #5a5a7a;
  --km-accent: #8b8bff; /* soft violet */
}
```

### Atmospheric Effects

Depth comes from subtle environmental cues, not heavy decoration:

- **Grain overlays**: `filter: url(#grain)` or CSS noise via `background-image` with tiny SVG data-URI
- **Gradient washes**: Radial gradients at 5-10% opacity behind key sections
- **Blur layers**: `backdrop-filter: blur()` on overlapping panels (glassmorphism-lite)
- **Vignettes**: Subtle radial gradient at viewport edges on dark themes

---

## Animation System — GSAP Implementation

### Architecture & Setup

Always centralize GSAP initialization. Register plugins once:

```js
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { ScrollSmoother } from "gsap/ScrollSmoother";
import { SplitText } from "gsap/SplitText";

gsap.registerPlugin(ScrollTrigger, ScrollSmoother, SplitText);

// Smooth scroll wrapper (optional but recommended)
ScrollSmoother.create({
  smooth: 1.2,
  effects: true,
  normalizeScroll: true,
});
```

HTML structure for ScrollSmoother:
```html
<div id="smooth-wrapper">
  <div id="smooth-content">
    <!-- ALL CONTENT HERE -->
  </div>
</div>
```

### The Animation Toolkit

Build every page from these composable patterns:

#### 1. Entrance Reveals (Scroll-Triggered)

The bread and butter. Elements fade/slide into view as they enter the viewport.

```js
// Fade up — the workhorse
gsap.from(".reveal-up", {
  scrollTrigger: { trigger: ".reveal-up", start: "top 85%" },
  y: 40,
  opacity: 0,
  duration: 0.8,
  ease: "power2.out",
  stagger: 0.1,
});

// Fade from left
gsap.from(".reveal-left", {
  scrollTrigger: { trigger: ".reveal-left", start: "top 80%" },
  x: -60,
  opacity: 0,
  duration: 0.8,
  ease: "power3.out",
});

// Scale reveal (for images/cards)
gsap.from(".reveal-scale", {
  scrollTrigger: { trigger: ".reveal-scale", start: "top 85%" },
  scale: 0.9,
  opacity: 0,
  duration: 1,
  ease: "power2.out",
});
```

#### 2. Parallax Layers

Create depth by moving elements at different scroll speeds.

```html
<div data-speed="0.8">Slower background</div>
<div data-speed="1.2">Faster foreground</div>
```

Or manual parallax with ScrollTrigger:
```js
gsap.to(".parallax-bg", {
  scrollTrigger: {
    trigger: ".parallax-section",
    start: "top bottom",
    end: "bottom top",
    scrub: 1,
  },
  y: -120,
  ease: "none",
});
```

#### 3. Pinned Sections

Pin a section while content transforms within it. Ideal for storytelling sequences.

```js
const tl = gsap.timeline({
  scrollTrigger: {
    trigger: ".pin-section",
    start: "top top",
    end: "+=200%",
    scrub: 1,
    pin: true,
  },
});

tl.from(".pin-title", { opacity: 0, y: 60, duration: 1 })
  .from(".pin-description", { opacity: 0, y: 40, duration: 1 }, "-=0.5")
  .to(".pin-image", { scale: 1.1, duration: 2 }, "-=1");
```

#### 4. Horizontal Scroll Sections

Transform vertical scroll into horizontal movement for galleries or timelines.

```js
const sections = gsap.utils.toArray(".horizontal-panel");
gsap.to(sections, {
  xPercent: -100 * (sections.length - 1),
  ease: "none",
  scrollTrigger: {
    trigger: ".horizontal-container",
    pin: true,
    scrub: 1,
    end: () => "+=" + document.querySelector(".horizontal-container").offsetWidth,
  },
});
```

#### 5. Clip-Path / Mask Reveals

Reveal images or sections by animating `clipPath`.

```js
gsap.from(".clip-reveal", {
  scrollTrigger: { trigger: ".clip-reveal", start: "top 80%" },
  clipPath: "inset(100% 0% 0% 0%)",
  duration: 1.2,
  ease: "power4.out",
});
```

#### 6. Counter / Number Animations

For statistics or data-driven sections:

```js
gsap.from(".stat-number", {
  scrollTrigger: { trigger: ".stat-number", start: "top 85%" },
  textContent: 0,
  duration: 2,
  ease: "power1.out",
  snap: { textContent: 1 },
});
```

#### 7. Cursor-Reactive Elements

Subtle parallax or rotation that follows the cursor. Use sparingly.

```js
document.addEventListener("mousemove", (e) => {
  const x = (e.clientX / window.innerWidth - 0.5) * 20;
  const y = (e.clientY / window.innerHeight - 0.5) * 20;
  gsap.to(".cursor-react", { x, y, duration: 0.6, ease: "power2.out" });
});
```

---

## Micro-Interactions

Small motions that communicate state and create delight:

| Element | Interaction | Animation |
|---------|-------------|-----------|
| Buttons | Hover | Scale 1.03, subtle shadow lift, 0.3s `power2.out` |
| Links | Hover | Underline slides in from left via `scaleX`, color shift |
| Cards | Hover | Slight Y lift (-4px), shadow expansion, 0.35s |
| Nav items | Hover | Letter-spacing expand + opacity indicator |
| Images | Hover | Subtle scale 1.05 with `overflow: hidden` on parent |
| Inputs | Focus | Border color transition + label float, 0.25s |

### Hover Pattern (CSS-first, GSAP for complex):

```css
.km-button {
  transition: transform 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94),
              box-shadow 0.3s ease;
}
.km-button:hover {
  transform: translateY(-2px) scale(1.02);
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.12);
}
```

---

## Layout Patterns

### Section Templates

**Hero — Centered Statement**
Pinned hero with oversized headline. Text fades in letter-by-letter, background image parallaxes. Single CTA appears last.

**Content — Split Asymmetric**
60/40 or 70/30 image-text split. Image reveals via clipPath, text staggers in from the content side.

**Gallery — Elastic Grid**
Masonry or grid layout where columns scroll at different speeds (ScrollSmoother `data-lag`).

**Stats — Horizontal Counter Bar**
Pinned section with horizontal scroll. Numbers count up as each stat panel enters center viewport.

**Testimonials — Fade Carousel**
Single testimonial visible at a time. Crossfade with slight Y-shift on scroll or auto-advance.

**Footer — Reveal from Below**
Main content slides up and away, revealing a dark footer beneath (negative margin + clip technique).

### Spacing Scale

Use a consistent spacing system. Recommended 8px base:

```css
:root {
  --km-space-xs: 0.5rem;   /* 8px */
  --km-space-sm: 1rem;     /* 16px */
  --km-space-md: 2rem;     /* 32px */
  --km-space-lg: 4rem;     /* 64px */
  --km-space-xl: 8rem;     /* 128px */
  --km-space-2xl: 12rem;   /* 192px */
}
```

Sections should have `--km-space-xl` to `--km-space-2xl` vertical padding. Generous spacing IS the minimalism.

---

## Performance Rules

1. **Use `will-change` sparingly** — Only on elements about to animate. Remove after animation completes.
2. **Animate transforms and opacity only** — Never animate `width`, `height`, `top`, `left`, `margin`, or `padding`. These trigger layout recalculations.
3. **Lazy-load below-fold images** — Use `loading="lazy"` or Intersection Observer.
4. **Use WebP/AVIF** — Compress images aggressively. Motion should be the visual richness, not heavy assets.
5. **Respect `prefers-reduced-motion`** — Always provide a reduced-motion fallback:

```js
const prefersReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)").matches;

if (prefersReducedMotion) {
  gsap.globalTimeline.timeScale(0);
  // Or: skip all ScrollTrigger animations, show content immediately
  gsap.set(".reveal-up, .reveal-left, .reveal-scale", { clearProps: "all" });
}
```

6. **Keep ScrollTrigger instances tidy** — Kill triggers on route change (SPA). Store references and clean up:

```js
const triggers = [];
triggers.push(
  ScrollTrigger.create({ /* ... */ })
);
// Cleanup
triggers.forEach(t => t.kill());
```

7. **Test on mobile** — Use `normalizeScroll: true` on ScrollSmoother. Test touch scroll behavior on real devices.

---

## Responsive Motion Strategy

Not all animations should exist on all screens:

| Viewport | Approach |
|----------|----------|
| Desktop (>1024px) | Full animation suite: parallax, pinning, horizontal scroll, cursor effects |
| Tablet (768–1024px) | Reduce parallax intensity by 50%, remove cursor effects, simplify pins |
| Mobile (<768px) | Entrance reveals only (fade-up). Remove parallax, pinning, horizontal scroll. Keep micro-interactions. |

```js
const mm = gsap.matchMedia();

mm.add("(min-width: 1024px)", () => {
  // Desktop animations
});

mm.add("(max-width: 1023px)", () => {
  // Simplified mobile animations
});
```

---

## Implementation Checklist

Before shipping a Kinetic Minimalism page, verify:

- [ ] All animations serve a narrative purpose (guide, reveal, emphasize, delight)
- [ ] One hero moment per viewport — no competing animations
- [ ] Consistent easing across the page (don't mix 5 different ease curves)
- [ ] Stagger values feel rhythmic, not random
- [ ] `prefers-reduced-motion` is respected
- [ ] 60fps on target devices (check with Chrome DevTools Performance tab)
- [ ] ScrollTrigger `markers: true` removed before deploy
- [ ] Images optimized (WebP, lazy-loaded)
- [ ] Mobile tested on real device (not just DevTools emulation)
- [ ] No layout shifts (CLS) caused by animations
- [ ] Font loading doesn't cause FOUT that breaks kinetic type

---

## Quick-Start Template

For a new Kinetic Minimalism page, start with this structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kinetic Minimalism</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <!-- Load display + body font pair -->
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    :root {
      /* Palette */
      --km-bg: #0a0a0f;
      --km-surface: #14141c;
      --km-text: #f0ece4;
      --km-muted: #6b6b7b;
      --km-accent: #c9a96e;
      /* Spacing */
      --km-space-lg: 4rem;
      --km-space-xl: 8rem;
      /* Motion */
      --km-duration: 0.8s;
    }
    html, body { background: var(--km-bg); color: var(--km-text); font-family: 'Your Body Font', sans-serif; }
    section { padding: var(--km-space-xl) var(--km-space-lg); }
    .hero-title { font-family: 'Your Display Font', serif; font-size: clamp(3rem, 8vw, 7rem); line-height: 1.05; }
  </style>
</head>
<body>
  <div id="smooth-wrapper">
    <div id="smooth-content">
      <section class="hero">
        <h1 class="hero-title">Your Statement</h1>
        <p class="hero-subtitle reveal-up">Supporting line</p>
      </section>
      <!-- More sections -->
    </div>
  </div>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
  <!-- Add ScrollSmoother, SplitText if using Club plugins -->
  <script>
    gsap.registerPlugin(ScrollTrigger);
    // Initialize animations here
  </script>
</body>
</html>
```

---

## Reference Files

For deeper guidance on specific areas, read these references:

- `references/easing-guide.md` — Complete easing curve recommendations by context
- `references/animation-patterns.md` — Extended code examples for all 7 animation patterns
- `references/responsive-motion.md` — Detailed breakpoint strategy and `gsap.matchMedia()` patterns
