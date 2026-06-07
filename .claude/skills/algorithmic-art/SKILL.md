---
name: algorithmic-art
description: Creates generative art using p5.js with seeded randomness and interactive parameter exploration. Follows a two-phase process — first developing a computational aesthetic philosophy, then implementing it as a self-contained interactive HTML artifact with seed navigation.
license: Complete terms in LICENSE.txt
---

# Algorithmic Art

Creates generative art as self-contained interactive HTML artifacts using p5.js with reproducible seeded randomness.

## Two-Phase Process

### Phase 1: Algorithmic Philosophy

Write a computational aesthetic manifesto (4–6 paragraphs) articulating an emergent visual system through:
- Mathematical beauty and pattern
- Emergent behavior from simple rules
- Seeded variation and reproducibility
- Compositional qualities: rhythm, tension, density, flow

The philosophy must stress that the final algorithm should appear as though it took countless hours to develop, refined with meticulous care. Implementation should avoid copying existing artists' styles — create original compositions.

### Phase 2: p5.js Implementation

Express the philosophy as code. The algorithm flows from the philosophy — not from a menu of preset patterns.

## Technical Requirements

- Start from `templates/viewer.html` as the foundation
- Keep fixed: layout structure, Anthropic branding, seed navigation controls
- Replace only: the p5.js algorithm, parameters object, and UI controls
- Output: single self-contained HTML artifact with p5.js from CDN

## Seeded Randomness

All artwork must use `randomSeed()` and `noiseSeed()` for reproducible variations:

```js
let seed = 42;

function setup() {
  randomSeed(seed);
  noiseSeed(seed);
  // ...
}
```

Always include: seed display, prev/next/random seed buttons, regenerate/reset actions.

## Parameter Design

Design parameters as tunable qualities, not preset patterns:
- Quantities (how many elements)
- Scales and ratios (size relationships)
- Probabilities (chance of variation)
- Angles and thresholds (geometry)
- Timing and rhythm (for animated work)

Parameters emerge from the algorithmic philosophy, not the other way around.

## Craftsmanship Standard

The implemented algorithm must:
- Appear as though it took countless hours to develop
- Be refined with care — not a first draft
- Have conceptual depth that remains subtle, not obvious
- Produce compositions that feel discovered, not designed

## Example Philosophy Directions

- *Recursive Crystallography* — forms that grow like mineral structures
- *Stochastic Weaving* — probabilistic interlacing of paths
- *Cellular Erosion* — rules that simulate geological wear
- *Harmonic Interference* — wave patterns that create moiré effects
