# CLAUDE.md — Rust Project Template

<!-- Copy this file to your project root as CLAUDE.md and customize it. -->

## Project Overview

- **Name:** <!-- Your project name -->
- **Description:** <!-- One-liner about what this project does -->
- **Type:** Binary <!-- or Library, Workspace -->
- **Rust edition:** 2021
- **MSRV:** 1.75 <!-- minimum supported Rust version, adjust as needed -->

## Commands

| Action | Command |
|--------|---------|
| Build (debug) | `cargo build` |
| Build (release) | `cargo build --release` |
| Run | `cargo run` |
| Run (release) | `cargo run --release` |
| Run tests | `cargo test` |
| Run single test | `cargo test test_name` |
| Lint | `cargo clippy -- -D warnings` |
| Format | `cargo fmt` |
| Check (fast compile check) | `cargo check` |
| Doc generation | `cargo doc --open` |
| Audit deps | `cargo audit` |
| Update deps | `cargo update` |

## Project Structure

```
src/
├── main.rs           # Entry point (binary) or lib.rs (library)
├── config.rs         # Configuration and CLI args
├── error.rs          # Custom error types (thiserror)
├── models/           # Data structures and types
│   └── mod.rs
├── services/         # Business logic
│   └── mod.rs
├── handlers/         # Request handlers (if web)
│   └── mod.rs
└── utils/            # Shared utilities
    └── mod.rs
tests/
├── integration/      # Integration tests
│   └── mod.rs
benches/              # Benchmarks (criterion)
```

## Conventions

- Use `thiserror` for library errors, `anyhow` for application errors.
- Prefer `&str` over `String` in function parameters.
- Use `clippy` with `-D warnings` — treat all warnings as errors.
- Naming: `snake_case` for functions/variables/modules, `PascalCase` for types/traits, `SCREAMING_SNAKE` for constants.
- Error handling: use `?` operator, avoid `.unwrap()` in production code (use `.expect("reason")` if necessary).
- Use `#[derive(Debug, Clone)]` on all public types.
- Group imports: std first, external crates second, crate-local third.
- Document all public items with `///` doc comments.

## Key Dependencies

<!-- List your main crates here so Claude knows what's available -->

| Crate | Purpose |
|-------|---------|
| `tokio` | Async runtime |
| `serde` / `serde_json` | Serialization |
| `clap` | CLI argument parsing |
| `tracing` | Structured logging |
| `reqwest` | HTTP client |
| `sqlx` | Database access (async) |

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `DATABASE_URL` | Yes | Database connection string |
| `RUST_LOG` | No | Log level filter (e.g., `info,my_crate=debug`) |
| `PORT` | No | Server port (default: 8080) |

## Known Issues / Notes

<!-- Add anything Claude should know: unsafe blocks, FFI, platform-specific code, etc. -->
