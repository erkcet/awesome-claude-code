# CLAUDE.md — React / Next.js Template

<!-- Copy this file to your project root as CLAUDE.md and customize it. -->

## Project Overview

- **Name:** <!-- Your project name -->
- **Description:** <!-- One-liner about what this project does -->
- **Stack:** Next.js 14+, React 18+, TypeScript
- **Router:** App Router <!-- or Pages Router -->
- **Styling:** Tailwind CSS <!-- or CSS Modules, styled-components, etc. -->
- **UI Library:** shadcn/ui <!-- or Radix, MUI, Chakra, etc. -->
- **Package manager:** pnpm <!-- or npm, yarn -->

## Commands

| Action | Command |
|--------|---------|
| Install deps | `pnpm install` |
| Dev server | `pnpm dev` |
| Build | `pnpm build` |
| Start prod | `pnpm start` |
| Run tests | `pnpm test` |
| Lint | `pnpm lint` |
| Type check | `pnpm tsc --noEmit` |

## Project Structure

```
src/
├── app/                  # App Router pages and layouts
│   ├── layout.tsx        # Root layout
│   ├── page.tsx          # Home page
│   ├── api/              # API routes (Route Handlers)
│   └── (auth)/           # Route groups
├── components/
│   ├── ui/               # Reusable UI primitives (Button, Input, etc.)
│   └── features/         # Feature-specific components
├── lib/                  # Utilities, helpers, config
├── hooks/                # Custom React hooks
├── types/                # Shared TypeScript types
└── styles/               # Global styles
public/                   # Static assets
```

## Conventions

- Use Server Components by default. Add `"use client"` only when needed (interactivity, hooks, browser APIs).
- Use named exports for components.
- Component files: `PascalCase.tsx`. Utility files: `camelCase.ts`.
- Colocation: keep component-specific types, utils, and tests next to the component.
- Data fetching: use `fetch` in Server Components, React Query / SWR for client-side.
- Forms: use Server Actions with `useFormState` / `useFormStatus`.
- Avoid prop drilling — use composition or context at the feature level.

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `DATABASE_URL` | Yes | Database connection string |
| `NEXTAUTH_SECRET` | Yes | NextAuth.js secret |
| `NEXTAUTH_URL` | No | App URL (auto-detected in Vercel) |

## Known Issues / Notes

<!-- Add anything Claude should know: WIP areas, tech debt, gotchas -->
