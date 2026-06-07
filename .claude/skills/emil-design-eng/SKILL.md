---
name: emil-design-eng
description: Emil Kowalski's design engineering philosophy. UI polish, component animation, and the subtle details that make software feel great. Covers animation decision frameworks, easing, timing, button feedback, popover positioning, and performance.
---

# Emil Design Engineering

Design engineering principles focused on UI polish and the subtle details that make software feel exceptional.

## Core Philosophy

Taste is trained, not innate. Unseen details compound into experiences people love or hate. Beauty is a legitimate competitive advantage in software.

## Animation Decision Framework

Before adding any animation, ask:
1. Should this animate? (Does motion add meaning or is it decoration?)
2. What is its purpose? (Feedback, spatial orientation, delight?)
3. What easing? (Entrance vs exit vs state change)
4. How fast? (Under 300ms for UI; under 150ms for interaction feedback)

## Critical Principles

### What NOT to animate

- Never animate keyboard-initiated actions — these fire 100+ times per day
- Never start animations from `scale(0)` — they feel like they appeared from nowhere
- Never use `ease-in` for entrances — it feels sluggish

### Easing

- Use `ease-out` for entrances — element decelerates to rest
- Use `ease-in` for exits — element accelerates away (less common)
- Use springs for gesture interactions — they feel more natural than curves

### Timing

- UI animations: under 300ms
- Interaction feedback (button press): under 150ms
- Stagger delays: 30–60ms between items in a list

### Animate only compositor properties

For performance, only animate:
- `transform` (translate, scale, rotate)
- `opacity`

Never animate: `width`, `height`, `top`, `left`, `margin`, `padding`, `background`, `color` on large surfaces.

## Component Practices

### Buttons

- Must have `:active` scale feedback: `transform: scale(0.97)`
- The press should feel instantaneous — keep under 100ms

### Popovers and Menus

- Scale from their trigger element origin
- Exception: modals scale from center
- Use `@starting-style` for modern CSS entry animations

### Entry Animations

```css
@starting-style {
  .popover { opacity: 0; transform: scale(0.95); }
}
```

### List Animations

- Use stagger: each item delays by 30–60ms
- Keep per-item duration short: 200–250ms

## Advanced Techniques

- `clip-path` reveals for creative entrance effects
- `blur()` to mask imperfect crossfades (keep ≤8px, short duration)
- CSS variables for inheritance-aware animations
- Momentum-based dismissal for drag interactions

## Performance and Accessibility

- Test on real devices — simulator performance does not reflect reality
- Always respect `prefers-reduced-motion`
- Hardware acceleration: trigger with `transform: translateZ(0)` only when necessary

## Review Checklist

- [ ] Does every button have `:active` feedback?
- [ ] Are animations under 300ms?
- [ ] Is `ease-out` used for entrances?
- [ ] Are only `transform` and `opacity` being animated?
- [ ] Does it feel right on a mid-range phone?
- [ ] Is `prefers-reduced-motion` respected?
- [ ] Do popovers scale from their trigger?
