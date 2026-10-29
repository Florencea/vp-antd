---
trigger: glob
globs: "src/routes/**"
description: TanStack Router route topology, route tree protection, and navigation conventions.
---

# Routing Guidelines (TanStack Router)

Guidelines for file-based routing with TanStack Router in this repository.

## 1. Route Topology

Place route modules strictly under `src/routes/`:

- `/`: Clean starter landing page with runtime telemetry (`src/routes/index.tsx`).
- `/canary`: Dedicated regression testbed for Ant Design + Tailwind CSS integration points (`src/routes/canary.tsx`).
- `/$`: Catch-all wildcard route redirecting back to `/` (`src/routes/$.tsx`).

## 2. Route Tree Protection & Synchronization

- **Protected File**: NEVER manually edit `src/routeTree.gen.ts`. It is automatically generated and synchronized by `@tanstack/router-plugin/vite`.
- **Regeneration**: Trigger route tree regeneration via `vpr agent:verify:inner` or `vp build`.
