---
name: web-artifacts-builder
description: Suite of tools for creating elaborate, multi-component claude.ai HTML artifacts using modern frontend web technologies (React, Tailwind CSS, shadcn/ui). Bundles everything into a single self-contained HTML file.
license: Complete terms in LICENSE.txt
---

# Web Artifacts Builder

Creates sophisticated self-contained HTML artifacts for claude.ai using React 18 + TypeScript + Vite + Tailwind CSS + shadcn/ui. All assets inline into a single HTML file.

## Stack

- React 18 + TypeScript
- Vite (development) + Parcel (bundling)
- Tailwind CSS 3.4.1
- shadcn/ui (40+ pre-installed components)
- Path alias: `@/` → `src/`

## Workflow

1. **Initialize** — run `scripts/init-artifact.sh` to scaffold the project
2. **Develop** — build your components in `src/`
3. **Bundle** — run `scripts/bundle-artifact.sh` to produce a single HTML file
4. **Share** — the output HTML has all JS, CSS, and deps inlined

## Design Guidance

Avoid common AI aesthetic pitfalls:
- No excessive centered layouts
- No purple gradients
- No uniform 8px rounded corners on everything
- No Inter as the only font

Use the shadcn/ui component library for consistent, accessible UI primitives. See https://ui.shadcn.com/docs/components for available components.

## Testing

Present the artifact first. Only test with Playwright if there's a specific issue or the user requests verification. Avoid upfront testing — it adds latency before the user can see the result.

## Key Notes

- The bundle step inlines all assets — the output is fully portable
- shadcn/ui components are already installed — use them directly
- TypeScript path aliases (`@/components`, `@/lib/utils`) work out of the box
- Tailwind CSS theming is preconfigured and compatible with shadcn/ui tokens
