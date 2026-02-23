# CLAUDE.md — Go Project Template

<!-- Copy this file to your project root as CLAUDE.md and customize it. -->

## Project Overview

- **Name:** <!-- Your project name -->
- **Description:** <!-- One-liner about what this project does -->
- **Go version:** >= 1.22
- **Module path:** `github.com/yourorg/yourproject`

## Commands

| Action | Command |
|--------|---------|
| Run | `go run ./cmd/server` |
| Build | `go build -o bin/server ./cmd/server` |
| Run tests | `go test ./...` |
| Run tests (verbose) | `go test -v ./...` |
| Run single test | `go test -run TestName ./path/to/package` |
| Test with race detector | `go test -race ./...` |
| Lint | `golangci-lint run` |
| Format | `gofmt -w .` |
| Tidy modules | `go mod tidy` |
| Vet | `go vet ./...` |
| Generate | `go generate ./...` |

## Project Structure

```
cmd/
├── server/           # Main application entry point
│   └── main.go
internal/             # Private application code
├── config/           # Configuration loading
├── handler/          # HTTP handlers
├── middleware/        # HTTP middleware
├── model/            # Data models / domain types
├── repository/       # Database access layer
├── service/          # Business logic
└── testutil/         # Test helpers and fixtures
pkg/                  # Public library code (if any)
api/                  # API definitions (OpenAPI, protobuf)
migrations/           # Database migrations (SQL files)
```

## Conventions

- Follow [Effective Go](https://go.dev/doc/effective_go) and the [Go Code Review Comments](https://go.dev/wiki/CodeReviewComments).
- Use `internal/` for all application code; `pkg/` only for truly reusable libraries.
- Naming: `camelCase` for unexported, `PascalCase` for exported, short variable names in small scopes.
- Error handling: always check errors, wrap with `fmt.Errorf("context: %w", err)`, use sentinel errors or custom types.
- Use `context.Context` as the first parameter for functions that do I/O.
- Interfaces should be small (1-3 methods) and defined by the consumer, not the implementer.
- Use table-driven tests. Test files are `*_test.go` in the same package.
- No init() functions unless absolutely necessary.

## Key Dependencies

| Package | Purpose |
|---------|---------|
| `net/http` | HTTP server (stdlib) |
| `database/sql` | Database access (stdlib) |
| `github.com/go-chi/chi` | HTTP router <!-- or gorilla/mux, gin, echo --> |
| `github.com/jackc/pgx/v5` | PostgreSQL driver |
| `go.uber.org/zap` | Structured logging |
| `github.com/stretchr/testify` | Test assertions |

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `DATABASE_URL` | Yes | PostgreSQL connection string |
| `PORT` | No | Server port (default: 8080) |
| `LOG_LEVEL` | No | Log level: debug, info, warn, error |
| `ENV` | No | Environment: development, production |

## Known Issues / Notes

<!-- Add anything Claude should know: cgo dependencies, build tags, etc. -->
