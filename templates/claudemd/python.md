# CLAUDE.md — Python Project Template

<!-- Copy this file to your project root as CLAUDE.md and customize it. -->

## Project Overview

- **Name:** <!-- Your project name -->
- **Description:** <!-- One-liner about what this project does -->
- **Stack:** Python 3.12+ <!-- add frameworks: FastAPI, Django, Flask, etc. -->
- **Package manager:** pip <!-- or poetry, uv, pdm -->
- **Virtual env:** `.venv/` (activate with `source .venv/bin/activate`)

## Commands

| Action | Command |
|--------|---------|
| Create venv | `python -m venv .venv` |
| Activate venv | `source .venv/bin/activate` |
| Install deps | `pip install -r requirements.txt` |
| Install dev deps | `pip install -r requirements-dev.txt` |
| Run app | `python -m src.main` |
| Run tests | `pytest` |
| Run tests (verbose) | `pytest -v --tb=short` |
| Lint | `ruff check .` |
| Format | `ruff format .` |
| Type check | `mypy src/` |

## Project Structure

```
src/
├── __init__.py
├── main.py           # Entry point
├── api/              # API routes / endpoints
├── services/         # Business logic
├── models/           # Data models (Pydantic, SQLAlchemy, etc.)
├── repositories/     # Database access layer
└── utils/            # Shared utilities
tests/
├── conftest.py       # Shared fixtures
├── test_api/         # API tests
└── test_services/    # Service layer tests
```

## Conventions

- Use type hints everywhere.
- Use `pathlib.Path` over `os.path`.
- Use `async def` for I/O-bound operations.
- Naming: `snake_case` for variables/functions/modules, `PascalCase` for classes, `UPPER_CASE` for constants.
- Tests: prefix test files with `test_`, use pytest fixtures over setUp/tearDown.
- Imports: stdlib first, third-party second, local third. Use absolute imports.

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `DATABASE_URL` | Yes | Database connection string |
| `SECRET_KEY` | Yes | Application secret key |
| `DEBUG` | No | Enable debug mode (default: false) |

## Known Issues / Notes

<!-- Add anything Claude should know: WIP areas, tech debt, gotchas -->
