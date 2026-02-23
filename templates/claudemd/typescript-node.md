# CLAUDE.md — TypeScript/Node.js Template

<!-- Copy this file to your project root as CLAUDE.md and customize it. -->

## Project Overview

- **Name:** <!-- Your project name -->
- **Description:** <!-- One-liner about what this project does -->
- **Stack:** TypeScript, Node.js <!-- add frameworks: Express, Fastify, NestJS, etc. -->
- **Node version:** >= 20
- **Package manager:** npm <!-- or pnpm, yarn -->

## Commands

| Action | Command |
|--------|---------|
| Install deps | `npm install` |
| Dev server | `npm run dev` |
| Build | `npm run build` |
| Run tests | `npm test` |
| Lint | `npm run lint` |
| Type check | `npx tsc --noEmit` |
| Format | `npx prettier --write .` |

## Project Structure

```
src/
├── index.ts          # Entry point
├── routes/           # API route handlers
├── services/         # Business logic
├── models/           # Data models / types
├── middleware/        # Express/Fastify middleware
├── utils/            # Shared utilities
└── config/           # Configuration and env validation
tests/
├── unit/             # Unit tests
└── integration/      # Integration tests
```

## Conventions

- Use named exports, no default exports.
- Use `async/await` over raw Promises.
- Error handling: throw typed errors, catch at route level.
- Naming: `camelCase` for variables/functions, `PascalCase` for types/classes, `SCREAMING_SNAKE` for constants.
- Tests: colocate unit tests as `*.test.ts` next to source files, or put in `tests/`.

## Environment Variables

<!-- List required env vars so Claude knows what the project needs -->

| Variable | Required | Description |
|----------|----------|-------------|
| `PORT` | No | Server port (default: 3000) |
| `DATABASE_URL` | Yes | PostgreSQL connection string |
| `NODE_ENV` | No | `development` / `production` |

## Known Issues / Notes

<!-- Add anything Claude should know: WIP areas, tech debt, gotchas -->
