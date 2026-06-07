---
name: shadcn
description: Work with shadcn/ui components — adding, searching, fixing, debugging, and styling. Use when working with shadcn/ui, component registries, or components.json. Applies when installing new components, composing UI with shadcn primitives, customizing variants, or debugging shadcn component behavior.
---

# shadcn/ui

shadcn/ui is a collection of reusable components built on Radix UI primitives, styled with Tailwind CSS. Components are added directly to your codebase via CLI — they're yours to own and modify.

## Core Rules

- **Reuse existing components** — check `components/ui/` before adding a new one
- **Compose, don't rebuild** — combine primitives (Button, Dialog, Form) rather than writing custom alternatives
- **Use built-in variants** — leverage `cva` variants defined in each component rather than overriding with arbitrary classes
- **Apply semantic color tokens** — use `bg-primary`, `text-foreground`, `border-input` etc., not raw Tailwind colors

## Adding Components

```bash
npx shadcn@latest add button
npx shadcn@latest add dialog form input label
npx shadcn@latest add --all   # add all components
```

Components land in `components/ui/`. Edit them freely.

## Component Catalog (commonly used)

| Component | Use case |
|-----------|----------|
| Button | Primary actions, variants: default/secondary/outline/ghost/destructive |
| Dialog | Modal overlays with focus trap |
| Sheet | Slide-in panel from edge |
| Command | Command palette / combobox |
| Form | React Hook Form + Zod validation wrapper |
| Input / Textarea | Text inputs |
| Select | Dropdown select |
| Popover | Floating content attached to trigger |
| Tooltip | Hover/focus information |
| Table | Data tables |
| Card | Content containers |
| Badge | Labels and status indicators |
| Alert | Inline notifications |
| Toast / Sonner | Transient notifications |
| Tabs | Tab navigation |
| Accordion | Expandable sections |
| Avatar | User images with fallback |
| Skeleton | Loading state placeholder |
| Separator | Visual dividers |
| Checkbox / Switch / RadioGroup | Form controls |
| DatePicker | Calendar-based date input |

## Theming

Colors are CSS variables in `globals.css`. Override in your theme:

```css
:root {
  --background: 0 0% 100%;
  --foreground: 222.2 84% 4.9%;
  --primary: 222.2 47.4% 11.2%;
  --primary-foreground: 210 40% 98%;
  /* ... */
}
```

Generate custom themes at https://ui.shadcn.com/themes

## Using `cn` Utility

```ts
import { cn } from "@/lib/utils"

<div className={cn("base-classes", condition && "conditional-class", className)} />
```

Always use `cn` (clsx + tailwind-merge) for conditional or merged class names.

## Form Pattern (React Hook Form + Zod)

```tsx
const form = useForm<z.infer<typeof schema>>({
  resolver: zodResolver(schema),
  defaultValues: { username: "" },
})

<Form {...form}>
  <FormField control={form.control} name="username" render={({ field }) => (
    <FormItem>
      <FormLabel>Username</FormLabel>
      <FormControl><Input {...field} /></FormControl>
      <FormMessage />
    </FormItem>
  )} />
</Form>
```

## components.json

Configuration file at project root. Specifies style, rsc, tsx, tailwind config, alias paths. Do not edit manually — use the CLI.

## Debugging

- If a component is missing, run `npx shadcn@latest add <name>`
- If styles look wrong, check that Tailwind CSS config includes the component paths
- If colors look wrong, verify CSS variables are defined for both `:root` and `.dark`
- Component source is in `components/ui/` — edit it if the default doesn't meet your needs
