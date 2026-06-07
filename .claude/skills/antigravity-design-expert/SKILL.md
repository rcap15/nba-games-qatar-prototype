---
name: antigravity-design-expert
description: Core UI/UX engineering skill for building highly interactive, spatial, weightless, and glassmorphism-based web interfaces using GSAP and 3D CSS. Use for immersive, motion-heavy interfaces with depth, floating cards, and scroll-driven animation.
risk: safe
source: community
date_added: "2026-03-07"
---

# Antigravity Design Expert

Builds interactive, spatial web interfaces with depth, glassmorphism, and smooth motion using GSAP and 3D CSS transforms.

## When to use

- Immersive landing pages, portfolio sites, interactive showcases
- Interfaces requiring spatial depth and floating elements
- Scroll-driven animations and parallax effects
- Glassmorphism card layouts

Do NOT use for conventional app UIs — this skill is for motion-heavy, immersive experiences specifically.

## Technology Stack

- **Framework**: React or Next.js
- **Styling**: Tailwind CSS + custom CSS for 3D transforms
- **Animation**: GSAP with ScrollTrigger
- **3D**: React Three Fiber or CSS `perspective` + `transform-style: preserve-3d`

## Design Philosophy

**Weightlessness**: Elements should appear to float through soft shadows, translucency, and spatial layering.

```css
.floating-card {
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
}
```

## GSAP Patterns

### ScrollTrigger entrance

```js
gsap.fromTo(".card", 
  { y: 60, opacity: 0 },
  {
    y: 0, opacity: 1,
    duration: 0.8,
    ease: "power2.out",
    stagger: 0.1,
    scrollTrigger: {
      trigger: ".cards-section",
      start: "top 80%",
    }
  }
);
```

### Hover float

```js
el.addEventListener("mouseenter", () => {
  gsap.to(el, { y: -8, duration: 0.3, ease: "power2.out" });
});
el.addEventListener("mouseleave", () => {
  gsap.to(el, { y: 0, duration: 0.4, ease: "power2.inOut" });
});
```

## 3D CSS Depth

```css
.scene {
  perspective: 1000px;
}
.card {
  transform-style: preserve-3d;
  transition: transform 0.4s ease-out;
}
.card:hover {
  transform: rotateY(8deg) rotateX(4deg) translateZ(20px);
}
```

## Animation Standards

- State transitions: smooth with `power2.out` or `power3.out` easing
- Staggered grid entrances: 0.08–0.12s between items
- Hover: 200–300ms; exit: 300–400ms (slightly slower)
- Always respect `prefers-reduced-motion`

```js
const prefersReduced = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
if (!prefersReduced) {
  // run GSAP animations
}
```

## Performance

- Use `will-change: transform` only during active animations, remove after
- Promote layers sparingly — many promoted layers cause memory issues
- Use `transform: translateZ(0)` only when needed for GPU compositing
- Test on mid-range mobile devices — desktop Chrome devtools are misleading

## Glassmorphism Guidelines

- Keep `backdrop-filter: blur()` between 8–20px
- Use sparingly — blur on large surfaces is expensive
- Ensure sufficient text contrast on translucent backgrounds (WCAG AA)
- Test on Safari — webkit prefix required: `-webkit-backdrop-filter`
