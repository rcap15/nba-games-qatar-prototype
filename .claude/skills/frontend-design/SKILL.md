---
name: frontend-design
description: Production-grade frontend design that avoids generic AI aesthetics. Creates distinctive, visually memorable interfaces with intentional typography, cohesive color, spatial composition, and functional beauty. Use when building UIs that need character and craftsmanship.
license: Complete terms in LICENSE.txt
---

# Frontend Design

Creates high-quality web interfaces with real aesthetic direction — not generic AI output.

## Design Thinking Framework

Before writing a single line, decide:

1. **Purpose** — What does this UI need to communicate or accomplish?
2. **Tone** — Pick a direction: brutalist/raw, art deco/geometric, minimalist/refined, maximalist/layered, retro/nostalgic, futuristic/clean, organic/natural, editorial/typographic
3. **Constraints** — Platform, audience, brand, accessibility requirements
4. **Differentiation** — What makes this memorable vs forgettable?

## Implementation Principles

- **Production-grade and functional** — code must work, not just look good
- **Visually striking and memorable** — commit to the aesthetic, don't hedge
- **Cohesive point-of-view** — every decision should serve the same direction
- **Extraordinary is possible** — don't hold back on creative ambition

## Aesthetic Guidelines

### Typography

- Choose fonts that are beautiful, unique, and interesting — avoid Inter, Roboto, or any generic default
- Use type as a design element, not just a vehicle for text
- Establish clear hierarchy: display → heading → body → caption
- Mix weights, sizes, and sometimes faces with intention
- Apply `text-balance` for headings, `text-pretty` for body

### Color and Theme

- Commit to a cohesive color system — don't use random colors
- Establish a dominant, a secondary, and an accent
- Consider: light vs dark, warm vs cool, saturated vs muted
- Use color meaningfully — not just decoratively

### Motion

- Prefer CSS-only solutions for most transitions
- Reserve JS animation for high-impact moments
- Keep transitions purposeful and short (150–300ms)
- Never add motion just to fill silence

### Spatial Composition

- Embrace unexpected layouts — full-bleed, asymmetry, overlap
- Generous whitespace is a design decision, not laziness
- Vertical rhythm creates visual calm
- Grid breaking creates visual energy — use intentionally

### Visual Details

- Create atmosphere through subtle texture, gradient, or shadow
- Details at small scale (icons, dividers, states) signal craft
- Hover/focus states are part of the design, not an afterthought
- Dark mode is not just color inversion — it's a different palette

## What to Avoid

Never produce:
- Generic centered hero + feature cards + footer layouts without a reason
- Purple, coral, or teal gradients as default brand expression
- Inter or Roboto as the only font choice
- Uniform rounded corners (8px) on everything
- Cookie-cutter design that lacks context-specific character
- Shadows that look copied from a Dribbble shot

## Review Checklist

- [ ] Does this have a clear, committed aesthetic direction?
- [ ] Would a designer at a top studio be proud of this?
- [ ] Are the font choices interesting and appropriate?
- [ ] Is the color system cohesive?
- [ ] Do spacing and layout feel considered, not default?
- [ ] Are interactive states (hover, focus, active) designed?
