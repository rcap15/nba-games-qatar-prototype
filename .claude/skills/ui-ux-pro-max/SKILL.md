---
name: ui-ux-pro-max
description: "UI/UX design intelligence for web and mobile. Includes 50+ styles, 161 color palettes, 57 font pairings, 161 product types, 99 UX guidelines, and 25 chart types across 10 stacks. Query design domains (product, style, typography, color, UX, charts, React Native, etc.) with reasoning rules applied automatically."
---

# UI/UX Pro Max

Comprehensive design intelligence framework for professional UI/UX across web and mobile platforms.

## Workflow

1. Analyze requirements — product type, stack, target device, context
2. Generate a design system with matching style, palette, and typography
3. Supplement with domain-specific searches for the relevant area (typography, charts, forms, etc.)
4. Apply stack-specific guidelines

## Rule Categories by Priority

| priority | category | impact |
|----------|----------|--------|
| 1 | accessibility | critical |
| 2 | touch and interaction | critical |
| 3 | performance | high |
| 4 | style selection | high |
| 5 | layout and responsive | high |
| 6 | typography and color | high |
| 7 | animation | medium |
| 8 | forms and feedback | high |
| 9 | navigation patterns | medium |
| 10 | charts and data | medium |

## Quick Reference

### 1. Accessibility (critical)

- Maintain WCAG AA contrast ratios (4.5:1 text, 3:1 large text)
- All interactive elements must be keyboard navigable
- Focus states must be clearly visible
- Never rely on color alone to convey information

### 2. Touch and Interaction (critical)

- Minimum 44×44pt touch targets with expanded hit areas
- Provide haptic feedback for important interactions on native platforms
- Swipe and gesture patterns must match platform conventions
- Avoid hover-only interactions on touch surfaces

### 3. Performance (high)

- Lazy load images and off-screen content
- Minimize layout shifts (CLS)
- Optimize critical rendering path
- Skeleton screens over spinners for content loading

### 4. Style Selection (high)

- Maintain visual consistency across a single design language
- Use vector-based icon assets — no emoji-only icons
- Adapt style to platform (iOS, Android, Web) conventions
- Choose from 50+ established styles: minimal, brutalist, material, glassmorphism, neumorphism, etc.

### 5. Layout and Responsive (high)

- Configure viewport correctly (`meta viewport`)
- Use a consistent breakpoint system (mobile-first preferred)
- Grid systems should be semantic and predictable
- Avoid fixed pixel layouts — use relative units

### 6. Typography and Color (high)

- Use semantic color tokens (primary, surface, error, etc.)
- Choose accessible, complementary font pairings — avoid generic defaults
- Support dynamic type / system font scaling
- Apply `text-balance` for headings, `text-pretty` for body

### 7. Animation (medium)

- Micro-interactions: 150–300ms timing
- Entrance: ease-out; exit: ease-in
- Respect `prefers-reduced-motion`
- Animate only compositor properties (transform, opacity)

### 8. Forms and Feedback (high)

- Always use visible labels (not placeholder-only)
- Show errors adjacent to the relevant field
- Use progressive disclosure for complex forms
- Provide confirmation for destructive actions

### 9. Navigation Patterns (medium)

- Limit bottom navigation to 5 items or fewer
- Support deep linking and back navigation
- Back button must restore prior state
- Tab order must follow visual reading order

### 10. Charts and Data (medium)

- Use accessible, colorblind-safe palettes for charts
- Include tooltips and legends for all data visualizations
- Label axes clearly
- Apply `tabular-nums` for numeric data
