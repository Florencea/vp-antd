---
trigger: glob
globs: "src/components/**, src/routes/**, src/theme.ts, src/global.css"
description: Ant Design v6 and TailwindCSS v4 SSOT design token bridge and styling rules.
---

# UI & Styling Architecture Guidelines

Guidelines for building UI components with Ant Design v6 and TailwindCSS v4 in this repository.

## 1. Single Source of Truth (SSOT)

- **Design Tokens**: TailwindCSS v4 `@theme` in `src/global.css` is the sole source of truth for design tokens (colors, breakpoints, etc.).
- **Dynamic Token Bridging**: `src/theme.ts` dynamically extracts CSS variables via `useSyncExternalStore` and `MutationObserver` on `document.documentElement` into Ant Design tokens (`useAntdTheme()`). Never provide hardcoded fallback colors in component styles.

## 2. Component Styling Rules

- **No Inline `style`**: Never use `style={{ ... }}` on Ant Design or React components. Prefer Ant Design layout components (`Layout`, `Flex`, `Space`, `Row`, `Col`, `Card`).
- **No `!` (important)**: Never use the `!` modifier in Tailwind classes. Tailwind utilities are scoped under `#root` in `src/global.css`, giving them natural specificity over Ant Design styles.
- **Canonical Classes**: Use Tailwind CSS v4 canonical class syntax. Run `vpr agent:lint:tailwind` to diagnose non-canonical classes and `vpr agent:lint:tailwind:fix` to automatically format them.
