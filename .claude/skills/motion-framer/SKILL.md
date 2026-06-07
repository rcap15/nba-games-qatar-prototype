---
name: motion-framer
description: Modern animation library for React and JavaScript. Create smooth, production-ready animations with motion components, variants, gestures, layout animations, AnimatePresence exit animations, spring physics, and scroll-based effects.
---

# Motion / Framer Motion

Production-ready animation library for React. Declarative API with hardware-accelerated transforms.

## Core Concepts

### Motion Components

Wrap any HTML element with `motion.*` to enable animation:

```jsx
import { motion } from "motion/react";

<motion.div animate={{ opacity: 1, x: 0 }} initial={{ opacity: 0, x: -20 }} />
```

### Animate Prop

Defines the target animation state. Runs whenever the value changes:

```jsx
<motion.div animate={{ scale: isOpen ? 1 : 0.8, opacity: isOpen ? 1 : 0 }} />
```

### Transitions

Control timing, type, and physics:

```jsx
<motion.div
  animate={{ x: 100 }}
  transition={{ type: "spring", stiffness: 300, damping: 30 }}
/>
// or tween:
transition={{ duration: 0.3, ease: "easeOut" }}
```

### Variants

Organize animation states with child propagation:

```jsx
const container = {
  hidden: { opacity: 0 },
  visible: { opacity: 1, transition: { staggerChildren: 0.1 } },
};

const item = {
  hidden: { y: 20, opacity: 0 },
  visible: { y: 0, opacity: 1 },
};

<motion.ul variants={container} initial="hidden" animate="visible">
  {items.map(i => <motion.li key={i} variants={item} />)}
</motion.ul>
```

## Common Patterns

### Hover and Tap

```jsx
<motion.button whileHover={{ scale: 1.05 }} whileTap={{ scale: 0.97 }}>
  Click me
</motion.button>
```

### Drag

```jsx
<motion.div drag dragConstraints={{ left: -100, right: 100, top: -50, bottom: 50 }} />
```

### Exit Animations (AnimatePresence)

```jsx
import { AnimatePresence, motion } from "motion/react";

<AnimatePresence>
  {isVisible && (
    <motion.div
      key="modal"
      initial={{ opacity: 0, scale: 0.95 }}
      animate={{ opacity: 1, scale: 1 }}
      exit={{ opacity: 0, scale: 0.95 }}
    />
  )}
</AnimatePresence>
```

### Layout Animations

```jsx
<motion.div layout />  // auto-animates layout changes
```

### Scroll-based (whileInView)

```jsx
<motion.div
  initial={{ opacity: 0, y: 40 }}
  whileInView={{ opacity: 1, y: 0 }}
  viewport={{ once: true }}
/>
```

### Spring Physics

```jsx
transition={{ type: "spring", stiffness: 400, damping: 17 }}
```

## Hooks

- `useAnimate()` — imperative animation API
- `useSpring(value)` — spring-driven MotionValue
- `useInView(ref)` — boolean for viewport intersection

## Performance

- Animate only `transform` and `opacity` — they run on the compositor
- Never animate `width`, `height`, `top`, `left`, `margin`, or `padding`
- Use `will-change` sparingly and only during active animations
- Prefer `layout` prop over animating position properties

## Accessibility

- Always respect `prefers-reduced-motion`:

```jsx
import { useReducedMotion } from "motion/react";
const shouldReduceMotion = useReducedMotion();
```

## Common Pitfalls

- Do not animate `display` — use `opacity` + `pointer-events: none` instead
- `AnimatePresence` requires `key` on children to detect mount/unmount
- Springs have no fixed duration — use `duration` transition if you need exact timing
- `layout` animations can cause unexpected shifts when parent resizes
