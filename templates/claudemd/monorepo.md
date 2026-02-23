# CLAUDE.md — Monorepo Template

<!-- Copy this file to your project root as CLAUDE.md and customize it. -->

## Project Overview

- **Name:** <!-- Your project name -->
- **Description:** <!-- One-liner about what this project does -->
- **Stack:** TypeScript <!-- primary language, add others as needed -->
- **Monorepo tool:** Turborepo <!-- or Nx, Lerna, pnpm workspaces, Rush -->
- **Package manager:** pnpm <!-- or npm, yarn -->
- **Node version:** >= 20

## Packages

| Package | Path | Description |
|---------|------|-------------|
| `@scope/web` | `apps/web` | Next.js frontend |
| `@scope/api` | `apps/api` | Express/Fastify backend |
| `@scope/ui` | `packages/ui` | Shared component library |
| `@scope/config` | `packages/config` | Shared ESLint, TS, Tailwind configs |
| `@scope/db` | `packages/db` | Prisma schema and client |
| `@scope/utils` | `packages/utils` | Shared utility functions |

## Commands

| Action | Command | Scope |
|--------|---------|-------|
| Install all deps | `pnpm install` | Root |
| Dev (all) | `pnpm dev` | All apps |
| Dev (single) | `pnpm --filter @scope/web dev` | Single package |
| Build all | `pnpm build` | All packages |
| Build (single) | `pnpm --filter @scope/api build` | Single package |
| Test all | `pnpm test` | All packages |
| Test (single) | `pnpm --filter @scope/web test` | Single package |
| Lint all | `pnpm lint` | All packages |
| Type check all | `pnpm typecheck` | All packages |
| Add dep to package | `pnpm --filter @scope/web add <pkg>` | Single package |

## Project Structure

```
.
├── apps/
│   ├── web/              # Next.js frontend
│   │   ├── src/
│   │   ├── package.json
│   │   └── tsconfig.json
│   └── api/              # Backend API
│       ├── src/
│       ├── package.json
│       └── tsconfig.json
├── packages/
│   ├── ui/               # Shared component library
│   │   ├── src/
│   │   └── package.json
│   ├── config/           # Shared configs (ESLint, TS, Tailwind)
│   │   ├── eslint/
│   │   ├── typescript/
│   │   └── package.json
│   ├── db/               # Database schema and client
│   │   ├── prisma/
│   │   └── package.json
│   └── utils/            # Shared utilities
│       ├── src/
│       └── package.json
├── turbo.json            # Turborepo pipeline config
├── pnpm-workspace.yaml   # Workspace definitions
├── package.json          # Root scripts and devDependencies
└── tsconfig.json         # Base TypeScript config
```

## Conventions

- Every package has its own `package.json` and `tsconfig.json`.
- Shared packages are imported via `@scope/package-name` — never use relative paths across package boundaries.
- All packages export via their `package.json` `exports` field.
- Run commands from the root using `pnpm --filter <package>`.
- Database migrations run from the `packages/db` directory.
- Shared types live in `packages/utils/src/types/`.
- CI builds all packages on every PR; Turborepo caching avoids redundant work.

## Dependency Graph

```
apps/web  ─────> packages/ui
    │                │
    ├── packages/db  ├── packages/config
    │                │
    └── packages/utils <── apps/api
```

## Environment Variables

<!-- Each app/package manages its own .env file -->

| App | Variable | Required | Description |
|-----|----------|----------|-------------|
| `apps/web` | `NEXT_PUBLIC_API_URL` | Yes | Backend API URL |
| `apps/api` | `DATABASE_URL` | Yes | PostgreSQL connection string |
| `apps/api` | `JWT_SECRET` | Yes | Token signing secret |
| `packages/db` | `DATABASE_URL` | Yes | Same as api (shared) |

## Known Issues / Notes

<!-- Add anything Claude should know: cross-package gotchas, build order, etc. -->
- Run `pnpm install` from root after changing any `package.json`.
- Turborepo caches are in `node_modules/.cache/turbo` — delete if builds seem stale.
