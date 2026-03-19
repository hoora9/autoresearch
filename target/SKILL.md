---
name: codepen
description: CodePen Exploration & Code Sourcing
---



### Purpose
Before finalizing design decisions, explore CodePen to discover what's possible — find inspiration, evaluate interactive effects, and source production-ready code snippets for the website build.

### Browsing Workflow

#### 1. Explore Trending Pens
When looking for inspiration or evaluating what's possible:
- Use `web_fetch` to browse https://codepen.io/trending
- Review the trending pens for relevant UI patterns, animations, interactions, and layouts
- Identify pens that align with the project's visual direction and technical requirements

#### 2. Search for Specific Effects or Components
When the design team has a specific need (e.g., "scroll animation", "parallax hero", "glassmorphism card"):
- Use `web_fetch` to search: `https://codepen.io/search/pens?q={search_term}`
- Try multiple search terms to find the best options
- Example searches: "GSAP scroll animation", "3D card hover", "text reveal animation", "parallax section", "liquid gradient background"

#### 3. Browse Our Saved Pens
Check the team's existing collection first:
- Use `web_fetch` to browse https://codepen.io/your-work
- Review previously saved or created pens that may already solve the current need

#### 4. Extract Code from a Pen
Once a promising pen is found:
- Fetch the individual pen page to extract the HTML, CSS, and JavaScript
- Document the pen's URL for attribution
- Assess whether the code can be used as-is or needs adaptation for the project stack

### How to Use in the Design Process

1. **Discovery phase**: Browse trending and search broadly before committing to a design direction — present options to the team with links and descriptions
2. **Validation phase**: When the skill suggests an effect or interaction (e.g., "we want a kinetic text hero"), search CodePen to find working examples and assess feasibility
3. **Implementation phase**: Once a pen is selected, extract the code and adapt it to the project's tech stack, design system, and responsive requirements

### Important Notes

- Prefer pens that use vanilla JS or GSAP (our primary animation library) over framework-specific implementations
- If a pen uses dependencies, document them before integrating