# CLAUDE.md — SvelteKit Template

<!-- Copy this file to your project root as CLAUDE.md and customize it. -->

## Project Overview

- **Name:** <!-- Your project name -->
- **Description:** <!-- One-liner about what this project does -->
- **Stack:** SvelteKit 2.x, Svelte 5, TypeScript <!-- add extras: Tailwind, Drizzle, Lucia, etc. -->
- **Package manager:** npm <!-- or pnpm, bun -->
- **Node version:** 20+ (see `.nvmrc` if present)

## Commands

| Action | Command |
|--------|---------|
| Install deps | `npm install` |
| Dev server | `npm run dev` |
| Dev server (expose) | `npm run dev -- --host` |
| Build | `npm run build` |
| Preview build | `npm run preview` |
| Run tests (unit) | `npx vitest` |
| Run tests (e2e) | `npx playwright test` |
| Type check | `npm run check` |
| Lint | `npm run lint` |
| Format | `npm run format` |
| Add Svelte integration | `npx svelte-add@latest <integration>` |
| Database push (Drizzle) | `npx drizzle-kit push` |
| Generate migration | `npx drizzle-kit generate` |

## Project Structure

```
src/
├── app.html                  # HTML shell template
├── app.css                   # Global styles
├── app.d.ts                  # Global type declarations
├── hooks.server.ts           # Server hooks (auth, logging)
├── hooks.client.ts           # Client hooks (error handling)
├── lib/
│   ├── index.ts              # $lib entry point (re-exports)
│   ├── components/
│   │   ├── ui/               # Reusable UI primitives
│   │   └── layout/           # Layout components (Header, Footer)
│   ├── server/
│   │   ├── db.ts             # Database client
│   │   └── auth.ts           # Auth helpers (server-only via $lib/server)
│   ├── stores/               # Shared rune-based state
│   ├── utils/                # Utility functions
│   └── types/                # Shared TypeScript types
├── routes/
│   ├── +layout.svelte        # Root layout
│   ├── +layout.server.ts     # Root layout server load
│   ├── +page.svelte          # Home page
│   ├── +page.server.ts       # Home page server load / form actions
│   ├── +error.svelte         # Error page
│   ├── (app)/                # Route group (authenticated pages)
│   │   ├── dashboard/
│   │   │   ├── +page.svelte
│   │   │   └── +page.server.ts
│   │   └── settings/
│   │       ├── +page.svelte
│   │       └── +page.server.ts
│   ├── (auth)/               # Route group (login, register)
│   │   └── login/
│   │       ├── +page.svelte
│   │       └── +page.server.ts
│   └── api/                  # API routes (JSON endpoints)
│       └── health/
│           └── +server.ts
├── params/                   # Param matchers
│   └── id.ts
static/
├── favicon.png
└── robots.txt
tests/
├── unit/                     # Vitest unit tests
└── e2e/                      # Playwright end-to-end tests
```

## Conventions

- Use Svelte 5 runes: `$state()`, `$derived()`, `$effect()`, `$props()`. Do not use legacy `let` reactivity or `$:` statements.
- Data loading: use `+page.server.ts` `load` functions for server-side data. Use `+page.ts` only when data can load on both client and server.
- Form mutations: use SvelteKit form actions (`+page.server.ts` `actions`) with progressive enhancement via `use:enhance`. Avoid `fetch` POST for form submissions.
- Server-only code: place in `$lib/server/` to guarantee it never ships to the client.
- Components: one component per file, `PascalCase` filenames (e.g., `UserCard.svelte`). Props via `$props()`.
- Routing: file-based routing in `src/routes/`. Use route groups `(groupName)` for shared layouts without URL segments.
- Error handling: throw `error()` from load functions, use `+error.svelte` pages. Use `fail()` for form validation errors.
- Styling: use scoped `<style>` blocks per component. Global styles in `app.css`.
- Types: define shared types in `$lib/types/`. Use `PageData`, `ActionData` for page type safety.
- Environment variables: use `$env/static/private`, `$env/static/public`, `$env/dynamic/private`, or `$env/dynamic/public` — never `process.env`.

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `DATABASE_URL` | Yes | Database connection string |
| `AUTH_SECRET` | Yes | Secret for session signing |
| `PUBLIC_APP_URL` | No | Public-facing app URL (prefix `PUBLIC_` for client access) |
| `PUBLIC_SUPABASE_URL` | No | Supabase project URL |
| `PUBLIC_SUPABASE_ANON_KEY` | No | Supabase anonymous key |
| `REDIS_URL` | No | Redis connection string (sessions, cache) |
| `SMTP_HOST` | No | Email server hostname |
| `SENTRY_DSN` | No | Sentry error tracking DSN |
| `ORIGIN` | No | Trusted origin for CSRF (required in some adapters) |

## Known Issues / Notes

<!-- Add anything Claude should know: WIP areas, tech debt, gotchas -->
