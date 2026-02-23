# Awesome Claude Code [![Awesome](https://awesome.re/badge.svg)](https://awesome.re) [![GitHub stars](https://img.shields.io/github/stars/erkcet/awesome-claude-code?style=social)](https://github.com/erkcet/awesome-claude-code) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md) [![License: CC0-1.0](https://img.shields.io/badge/License-CC0_1.0-lightgrey.svg)](LICENSE) [![Links](https://github.com/erkcet/awesome-claude-code/actions/workflows/links.yml/badge.svg)](https://github.com/erkcet/awesome-claude-code/actions/workflows/links.yml)

> A curated list of resources, tools, tips, and community projects for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) — Anthropic's official agentic coding CLI.

Claude Code lives in your terminal, understands your codebase, and helps you code faster through natural language. Unlike simple code-completion tools, it can run commands, edit files across your project, manage git workflows, and orchestrate multi-step tasks autonomously.

**What makes this list different:** Every section includes copy-pasteable configs, working hook recipes, real templates, and practical examples — not just links.

**Contributions welcome!** Read the [contribution guidelines](CONTRIBUTING.md) before submitting a PR.

---

## Contents

- **Basics**
  - [Official Resources](#official-resources)
  - [Getting Started](#getting-started)
  - [CLI Usage & Reference](#cli-usage--reference)
- **Configuration**
  - [CLAUDE.md Templates](#claudemd-templates)
  - [Configuration Tools](#configuration-tools)
  - [Custom Slash Commands](#custom-slash-commands)
  - [Hooks](#hooks)
  - [Status Line Customization](#status-line-customization)
- **Extending**
  - [MCP Servers](#mcp-servers)
  - [Plugins](#plugins)
  - [Skills](#skills)
- **Agents & Orchestration**
  - [Subagents](#subagents)
  - [Multi-Agent Orchestration](#multi-agent-orchestration)
  - [Agent Teams](#agent-teams)
- **Workflows**
  - [Workflows & Patterns](#workflows--patterns)
  - [Automation & CI/CD](#automation--cicd)
  - [IDE Integrations](#ide-integrations)
  - [Usage Monitors & Cost Management](#usage-monitors--cost-management)
  - [Security & Permissions](#security--permissions)
- **Community**
  - [Community Projects](#community-projects)
  - [Articles & Blog Posts](#articles--blog-posts)
  - [Videos & Tutorials](#videos--tutorials)
  - [Community](#community)

---

## Official Resources

- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code) - Comprehensive official docs covering all features.
- [Claude Code GitHub](https://github.com/anthropics/claude-code) - Official repo, issue tracker, and discussions.
- [Claude Code Changelog](https://docs.anthropic.com/en/docs/claude-code/changelog) - Release notes and version history.
- [Claude Code Best Practices](https://docs.anthropic.com/en/docs/claude-code/best-practices) - Anthropic's recommended patterns for getting the most out of Claude Code.
- [Anthropic Cookbook](https://github.com/anthropics/anthropic-cookbook) - Official examples and guides from Anthropic.
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) - Official MCP specification and docs.
- [MCP Servers Repository](https://github.com/modelcontextprotocol/servers) - Official and community MCP server implementations.
- [Claude API Reference](https://docs.anthropic.com/en/api) - Underlying API that powers Claude Code.
- [Claude Code SDK](https://docs.anthropic.com/en/docs/claude-code/sdk) - Build custom agents and automations with the Claude Code SDK.
- [Anthropic Blog](https://www.anthropic.com/blog) - Engineering blog posts about Claude Code internals and best practices.

## Getting Started

- [Installation Guide](https://docs.anthropic.com/en/docs/claude-code/getting-started) - Official installation and setup instructions.
- [Claude Code Quickstart](https://docs.anthropic.com/en/docs/claude-code/quickstart) - Get up and running in minutes.
- [First Session Walkthrough](https://docs.anthropic.com/en/docs/claude-code/tutorials) - Step-by-step tutorial for your first coding session.
- [Claude Code Configuration](https://docs.anthropic.com/en/docs/claude-code/settings) - Settings, permissions, and environment configuration.
- [Memory & CLAUDE.md Guide](https://docs.anthropic.com/en/docs/claude-code/memory) - How Claude Code reads and uses memory files.

### Quick Install

```bash
# Install via npm (requires Node.js 18+)
npm install -g @anthropic-ai/claude-code

# Verify installation
claude --version

# Start your first session
cd your-project && claude

# Auto-generate a CLAUDE.md for your project
claude /init
```

## CLI Usage & Reference

### Interactive Commands

| Command | Description |
|---------|-------------|
| `/help` | Show all available commands |
| `/init` | Auto-generate a CLAUDE.md for the current project |
| `/compact` | Compress conversation history to free context |
| `/model <name>` | Switch model (opus, sonnet, haiku) |
| `/plan` | Enter plan mode — explore first, code second |
| `/review` | Review code changes |
| `/commit` | Create a git commit with a smart message |
| `/pr` | Create a GitHub pull request |
| `/cost` | Show token usage and estimated cost |
| `/clear` | Clear conversation history |
| `/fast` | Toggle fast mode (same model, faster output) |
| `/memory` | Edit CLAUDE.md memory files |

### CLI Flags

```bash
# One-shot query (non-interactive)
claude -p "What does the main function do?"

# Resume last conversation
claude --resume

# Resume specific session
claude --resume <session-id>

# List previous sessions
claude sessions list

# Use a specific model
claude --model opus
claude --model sonnet
claude --model haiku

# Headless mode (non-interactive, for scripts and CI)
claude -p "Run all tests and report results" --output-format json

# Stream output in headless mode
claude -p "Explain src/index.ts" --output-format stream-json

# Set max turns for autonomous operation
claude -p "Fix all lint errors" --max-turns 20

# Append system prompt
claude --system-prompt "Always respond in Spanish"

# Specify allowed tools
claude --allowedTools "Read,Write,Bash(git *)"

# Skip permissions (trusted projects only)
claude --dangerously-skip-permissions
```

### Piping & Scripting Patterns

```bash
# Review a PR diff
gh pr diff 123 | claude -p "Review this PR for bugs and security issues"

# Explain test failures
npm test 2>&1 | claude -p "Why are these tests failing? Suggest fixes."

# Analyze logs
tail -500 /var/log/app.log | claude -p "Summarize errors and suggest fixes"

# Generate commit message from staged changes
git diff --staged | claude -p "Write a conventional commit message" --output-format text

# Multi-file analysis
find src -name "*.ts" | head -20 | xargs cat | claude -p "Find potential memory leaks"

# Chain with other tools
claude -p "Generate a SQL migration to add a users table" --output-format text | pbcopy
```

### Session Management

```bash
# List recent sessions
claude sessions list

# Resume most recent session
claude --resume

# Resume specific session by ID
claude --resume abc123

# Continue with full context preserved
claude --continue
```

## CLAUDE.md Templates

> `CLAUDE.md` is the memory file Claude Code reads at session start. A good one dramatically improves output quality.

### Ready-to-Use Templates

- [Monorepo Template](templates/claudemd/monorepo.md) - Turborepo/Nx monorepos with multiple packages.
- [Python Project Template](templates/claudemd/python.md) - Python projects with venv, pytest, ruff, mypy.
- [TypeScript/Node Template](templates/claudemd/typescript-node.md) - Node.js/TypeScript with npm/pnpm, ESLint, Vitest.
- [React/Next.js Template](templates/claudemd/react-nextjs.md) - Next.js App Router with Tailwind and shadcn/ui.
- [Rust Project Template](templates/claudemd/rust.md) - Cargo-based Rust projects with clippy and testing.
- [Go Project Template](templates/claudemd/go.md) - Go modules with standard project layout.
- [Django Template](templates/claudemd/django.md) - Django projects with REST framework and celery.
- [SvelteKit Template](templates/claudemd/svelte.md) - SvelteKit projects with runes and form actions.
- [Laravel Template](templates/claudemd/laravel.md) - Laravel projects with Eloquent and artisan commands.
- [Data Science Template](templates/claudemd/data-science.md) - Jupyter notebooks, pandas, scikit-learn, experiment tracking.
- [Homelab/Infrastructure Template](templates/claudemd/homelab.md) - Server management, services, and infrastructure.
- [Mobile App Template](templates/claudemd/mobile.md) - React Native / Flutter cross-platform apps.

### CLAUDE.md Best Practices

- Keep it under 500 lines — Claude reads it every session, so conciseness matters.
- Put the most important context (build commands, architecture) at the top.
- Use tables for structured data (services, ports, API keys).
- Include the commands Claude should know how to run.
- Use nested `CLAUDE.md` files in subdirectories for package-specific context.
- Update it after every significant change to your project.
- Use comments (`<!-- -->`) to explain why, not just what.
- Include known issues and "don't touch" warnings for work-in-progress areas.

### CLAUDE.md Generator Prompt

> Paste this into Claude Code to auto-generate a CLAUDE.md tailored to your project:

```
Analyze this project and generate a CLAUDE.md file. Include:
1. Project overview (name, stack, description)
2. All available commands in a table (build, test, lint, run)
3. Project structure as a tree
4. Code conventions you observe (naming, imports, patterns)
5. Environment variables from .env.example or config files
6. Known issues from TODO/FIXME comments

Read package.json, tsconfig.json, Makefile, Cargo.toml, pyproject.toml,
or whatever build config exists. Be specific — use actual values, not placeholders.
```

### File Organization

```
project/
├── CLAUDE.md              # Root context — project-wide info
├── src/
│   ├── CLAUDE.md          # Source-specific conventions
│   ├── api/
│   │   └── CLAUDE.md      # API layer patterns and endpoints
│   └── components/
│       └── CLAUDE.md      # Component conventions, design system
├── .claude/
│   ├── settings.json      # Project-level Claude settings
│   └── commands/          # Custom slash commands
│       ├── review.md
│       └── deploy-check.md
└── tests/
    └── CLAUDE.md          # Testing conventions, fixtures
```

### What to Put in CLAUDE.md

| Section | Example |
|---------|---------|
| Project overview | "This is a Next.js 14 app with App Router" |
| Build/run commands | `npm run dev`, `npm test`, `npm run build` |
| Architecture | "We use the repository pattern with service layers" |
| Conventions | "Use named exports, no default exports" |
| Common tasks | "To add a new API route, create a file in `src/app/api/`" |
| Environment | "Requires Node 20+, PostgreSQL 16" |
| Known issues | "The auth module is being migrated, don't touch `legacy/`" |

## Configuration Tools

- [claude-config](https://github.com/anthropics/claude-code) - Built-in `/config` command to manage settings interactively.
- [dotenv-vault](https://github.com/dotenv-org/dotenv-vault) - Sync environment variables across machines for consistent Claude Code behavior.

### Settings Locations

| Scope | Path | Use Case |
|-------|------|----------|
| Global | `~/.claude/settings.json` | Personal defaults (permissions, model, hooks) |
| Global local | `~/.claude/settings.local.json` | Machine-specific overrides (not synced) |
| Project | `.claude/settings.json` | Shared team settings (commit to repo) |
| Project local | `.claude/settings.local.json` | Personal project overrides (gitignored) |

### Example: Project Settings

```jsonc
// .claude/settings.json — commit this to your repo
{
  "permissions": {
    "allow": [
      "Bash(npm run *)",
      "Bash(npx vitest *)",
      "Bash(git *)",
      "Read",
      "Write",
      "Edit"
    ],
    "deny": [
      "Bash(rm -rf *)",
      "Bash(curl *)",
      "Bash(wget *)"
    ]
  }
}
```

## Custom Slash Commands

> Place `.md` files in `.claude/commands/` to create project-specific commands. Use `$ARGUMENTS` to accept input.

### Example: `/project:review`

```markdown
<!-- .claude/commands/review.md -->
Review the changes in the current branch compared to main.
Focus on:
1. Security vulnerabilities
2. Performance regressions
3. Missing error handling
4. Test coverage gaps

Format as a markdown checklist with severity levels.
```

### Example: `/project:deploy-check`

```markdown
<!-- .claude/commands/deploy-check.md -->
Pre-deployment checklist:
1. Run all tests
2. Check for console.logs or debug statements
3. Verify environment variables are not hardcoded
4. Check for TODO/FIXME comments
5. Verify all API endpoints have error handling
6. Check bundle size hasn't increased significantly
```

### Example: `/project:doc`

```markdown
<!-- .claude/commands/doc.md -->
Generate documentation for $ARGUMENTS.
Include:
- Brief description of purpose
- Parameters with types and descriptions
- Return value
- Usage example
- Edge cases to be aware of

Write docs as JSDoc comments directly in the source file.
```

### Example: `/project:test`

```markdown
<!-- .claude/commands/test.md -->
Write comprehensive tests for $ARGUMENTS.
Include:
- Happy path tests
- Edge cases (empty input, null, undefined, boundary values)
- Error scenarios
- Integration points with mocked dependencies

Use the existing test patterns in this project.
```

## Hooks

> Hooks are shell commands that execute automatically in response to Claude Code events. Configure them in your settings JSON.

### Hook Events Reference

| Event | Trigger | Available Env Vars |
|-------|---------|-------------------|
| `PreToolUse` | Before any tool executes | `$CLAUDE_TOOL_NAME`, `$CLAUDE_FILE_PATH` |
| `PostToolUse` | After any tool executes | `$CLAUDE_TOOL_NAME`, `$CLAUDE_FILE_PATH`, `$CLAUDE_TOOL_OUTPUT` |
| `Notification` | When Claude sends a notification | `$CLAUDE_NOTIFICATION` |
| `Stop` | When Claude finishes a turn | — |

### Hook Configuration

```jsonc
// .claude/settings.json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "command": "echo 'About to run a shell command'"
      }
    ],
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "command": "eslint --fix \"$CLAUDE_FILE_PATH\" 2>/dev/null || true"
      }
    ],
    "Notification": [
      {
        "command": "terminal-notifier -message \"$CLAUDE_NOTIFICATION\" -title 'Claude Code'"
      }
    ],
    "Stop": [
      {
        "command": "say 'Claude is done'"
      }
    ]
  }
}
```

### Community Hook Recipes

**Auto-format on save (multi-language):**

```jsonc
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "command": "case \"$CLAUDE_FILE_PATH\" in *.py) black \"$CLAUDE_FILE_PATH\" 2>/dev/null;; *.ts|*.tsx|*.js|*.jsx) prettier --write \"$CLAUDE_FILE_PATH\" 2>/dev/null;; *.go) gofmt -w \"$CLAUDE_FILE_PATH\" 2>/dev/null;; *.rs) rustfmt \"$CLAUDE_FILE_PATH\" 2>/dev/null;; esac || true"
      }
    ]
  }
}
```

**Desktop notifications (macOS):**

```jsonc
{
  "hooks": {
    "Notification": [
      {
        "command": "osascript -e 'display notification \"'\"$CLAUDE_NOTIFICATION\"'\" with title \"Claude Code\"'"
      }
    ]
  }
}
```

**Block dangerous commands:**

```jsonc
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "command": "if echo \"$CLAUDE_TOOL_INPUT\" | grep -qE 'rm -rf /|DROP TABLE|format c:'; then echo 'BLOCKED: Dangerous command detected' >&2; exit 1; fi"
      }
    ]
  }
}
```

**Auto-run tests after edits:**

```jsonc
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "command": "if echo \"$CLAUDE_FILE_PATH\" | grep -qE '\\.(test|spec)\\.(ts|js|tsx|jsx)$'; then npx vitest run \"$CLAUDE_FILE_PATH\" --reporter=dot 2>/dev/null || true; fi"
      }
    ]
  }
}
```

## Status Line Customization

> Customize what Claude Code shows in the status bar at the bottom of your terminal.

```jsonc
// ~/.claude/settings.json
{
  "statusLine": {
    "enabled": true,
    "items": ["model", "cost", "session"]
  }
}
```

## MCP Servers

> MCP (Model Context Protocol) servers extend Claude Code with external tools and data sources. Add them to `.claude/settings.json` or `~/.claude/settings.json`.

### MCP Configuration Example

```jsonc
// .claude/settings.json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "ghp_your_token_here"
      }
    },
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres", "postgresql://localhost/mydb"]
    }
  }
}
```

### Official / First-Party

- [mcp-server-filesystem](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem) - Secure file system access with configurable permissions.
- [mcp-server-github](https://github.com/modelcontextprotocol/servers/tree/main/src/github) - GitHub API integration for repos, issues, PRs.
- [mcp-server-postgres](https://github.com/modelcontextprotocol/servers/tree/main/src/postgres) - Read-only PostgreSQL database access.
- [mcp-server-sqlite](https://github.com/modelcontextprotocol/servers/tree/main/src/sqlite) - SQLite database interaction and querying.
- [mcp-server-brave-search](https://github.com/modelcontextprotocol/servers/tree/main/src/brave-search) - Web search via Brave Search API.
- [mcp-server-puppeteer](https://github.com/modelcontextprotocol/servers/tree/main/src/puppeteer) - Browser automation and web scraping.
- [mcp-server-slack](https://github.com/modelcontextprotocol/servers/tree/main/src/slack) - Slack workspace integration.
- [mcp-server-memory](https://github.com/modelcontextprotocol/servers/tree/main/src/memory) - Persistent memory using a knowledge graph.
- [mcp-server-google-maps](https://github.com/modelcontextprotocol/servers/tree/main/src/google-maps) - Google Maps integration for location data.
- [mcp-server-fetch](https://github.com/modelcontextprotocol/servers/tree/main/src/fetch) - Fetch and convert web pages to markdown.
- [mcp-server-sequential-thinking](https://github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking) - Dynamic problem-solving through thought sequences.

### Community MCP Servers

- [mcp-server-docker](https://github.com/ckreiling/mcp-server-docker) - Manage Docker containers and images.
- [mcp-server-kubernetes](https://github.com/strowk/mcp-k8s-go) - Kubernetes cluster management.
- [mcp-server-linear](https://github.com/jerhadf/linear-mcp-server) - Linear issue tracker integration.
- [mcp-server-notion](https://github.com/v-3/notion-server) - Notion workspace access and page management.
- [mcp-server-raycast](https://github.com/raycast/mcp-server-raycast) - Raycast integration for macOS.
- [mcp-server-obsidian](https://github.com/smithery-ai/mcp-obsidian) - Obsidian vault access and note management.
- [mcp-server-todoist](https://github.com/abhiz123/todoist-mcp-server) - Todoist task management integration.
- [mcp-server-sentry](https://github.com/modelcontextprotocol/servers/tree/main/src/sentry) - Sentry error tracking integration.
- [mcp-server-turso](https://github.com/SilasMarvin/mcp-server-turso) - Turso/LibSQL database access.
- [mcp-server-supabase](https://github.com/supabase-community/supabase-mcp) - Supabase database and auth integration.

### MCP Resources

- [MCP Specification](https://spec.modelcontextprotocol.io/) - Full protocol specification.
- [Build Your Own MCP Server](https://modelcontextprotocol.io/quickstart/server) - Tutorial for creating custom MCP servers.
- [MCP TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk) - TypeScript SDK for building MCP servers.
- [MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk) - Python SDK for building MCP servers.

## Plugins

> Extend Claude Code's capabilities with community-built plugins and integrations.

- [claude-code-router](https://github.com/anthropics/claude-code) - Built-in model routing for cost optimization (use haiku for simple tasks, opus for complex ones).
- [claude-code-action](https://github.com/anthropics/claude-code-action) - GitHub Action for running Claude Code in CI/CD pipelines.

## Skills

> Skills are reusable prompt templates that Claude Code can invoke. They can be shared across projects and teams.

### Built-in Skills

| Skill | Trigger | Description |
|-------|---------|-------------|
| `/commit` | Git commit | Smart commit message generation |
| `/pr` | Pull request | Create PR with title, description, test plan |
| `/review` | Code review | Review current changes |
| `/init` | Initialize | Generate CLAUDE.md for current project |

### Custom Skills

Create custom skills in `.claude/commands/`:

```markdown
<!-- .claude/commands/migrate.md -->
Generate a database migration for $ARGUMENTS.
1. Check existing models and migrations for context
2. Create the migration file using the project's migration tool
3. Include both up and down migration logic
4. Add appropriate indexes for foreign keys
```

## Subagents

> Claude Code can spawn specialized subagents (via the Task tool) to handle parallel, isolated work. Subagents inherit project context but run in their own conversation.

### How Subagents Work

```
Main Agent
├── Task (Explore subagent) → "Find all API endpoints"
├── Task (Bash subagent) → "Run the full test suite"
└── Task (General subagent) → "Research how auth middleware works"
```

Subagents are useful for:
- **Parallel research** — explore multiple parts of a codebase simultaneously.
- **Isolated execution** — run tests or builds without cluttering the main conversation.
- **Context protection** — keep large tool outputs out of the main context window.

### Subagent Types

| Type | Best For |
|------|----------|
| `Explore` | Codebase exploration, finding files and patterns |
| `Bash` | Running commands, git operations |
| `general-purpose` | Multi-step research and code analysis |
| `Plan` | Designing implementation strategies |

## Multi-Agent Orchestration

> Use the Claude Code SDK to orchestrate multiple Claude Code instances for complex workflows.

### SDK Example: Parallel Code Review

```javascript
import { Claude } from "@anthropic-ai/claude-code";

const claude = new Claude();

// Review different aspects in parallel
const [security, performance, tests] = await Promise.all([
  claude.sendMessage("Review src/ for security vulnerabilities", {
    options: { model: "sonnet" }
  }),
  claude.sendMessage("Find performance bottlenecks in src/api/", {
    options: { model: "sonnet" }
  }),
  claude.sendMessage("Check test coverage gaps in src/services/", {
    options: { model: "haiku" }
  }),
]);

console.log("Security:", security.text);
console.log("Performance:", performance.text);
console.log("Tests:", tests.text);
```

### Headless Orchestration (Bash)

```bash
#!/bin/bash
# Run multiple Claude Code tasks in parallel

claude -p "Check for security issues in src/" --output-format json > /tmp/security.json &
claude -p "Find unused exports in src/" --output-format json > /tmp/unused.json &
claude -p "Identify slow database queries" --output-format json > /tmp/perf.json &

wait
echo "All reviews complete. Results in /tmp/*.json"
```

## Agent Teams

> For large projects, structure multiple Claude Code instances as a team with distinct roles.

### Example: Feature Development Team

| Role | Model | Responsibility |
|------|-------|---------------|
| Architect | Opus | Design the approach, break into subtasks |
| Implementer | Sonnet | Write the code based on the architect's plan |
| Reviewer | Sonnet | Review the implementer's code for quality |
| Tester | Haiku | Write and run tests for the new code |

```bash
# Step 1: Architect plans the approach
PLAN=$(claude -p "Plan how to add OAuth2 login. Output a numbered task list." \
  --model opus --output-format text)

# Step 2: Implementer writes code
claude -p "Implement this plan: $PLAN" --model sonnet

# Step 3: Reviewer checks the work
claude -p "Review all changes on this branch vs main" --model sonnet

# Step 4: Tester validates
claude -p "Write and run tests for the OAuth2 login feature" --model haiku
```

## Workflows & Patterns

### Plan Mode

Use plan mode for non-trivial tasks. It forces Claude to explore the codebase and design an approach before writing code.

```
> /plan Refactor the authentication module to use JWT instead of sessions
```

Plan mode is ideal for:
- Architecture changes affecting multiple files.
- Refactors where you want to review the approach first.
- Unfamiliar codebases where exploration is needed.

### Multi-Agent with Worktrees

Use git worktrees for parallel, isolated work:

```
> Work on the login page redesign in a worktree
> # Claude creates an isolated copy — your main branch stays clean
```

### Test-Driven Development (TDD)

```
> Write a failing test for user registration with email validation.
> Now implement the minimum code to make the test pass.
> Refactor the implementation while keeping tests green.
```

### Bug Investigation Pattern

```
> Read the error log below and trace the bug to its root cause.
> Don't fix it yet — just explain what's happening and which files are involved.
```

Then, once you understand the issue:

```
> Now fix the bug. Run the test suite after to confirm nothing else broke.
```

### Code Migration Pattern

```
> Migrate all class components in src/components/ to functional components with hooks.
> Do them one at a time. After each migration, run the tests for that component.
> Stop if any test fails.
```

### Effective Prompting Patterns

- **Be specific about scope**: "Fix the null check in `src/auth/login.ts:45`" > "Fix the login bug".
- **Reference files directly**: "Read `package.json` and update all outdated deps".
- **Chain tasks**: "Run the tests, fix any failures, then run them again".
- **Set constraints**: "Refactor this function but don't change the public API".
- **Ask for exploration first**: "What files handle payment processing?" before "Refactor payments".
- **Set quality gates**: "Run tests after every change. Stop if coverage drops below 80%".

### Git Workflow

```
> /commit                    # Smart commit with conventional message
> Create a PR for this branch # Generates title, description, test plan
```

## Automation & CI/CD

### GitHub Action: Claude Code Review

```yaml
# .github/workflows/claude-review.yml
name: Claude Code Review
on:
  pull_request:
    types: [opened, synchronize]

permissions:
  contents: read
  pull-requests: write

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - uses: anthropics/claude-code-action@v1
        with:
          anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
          prompt: |
            Review this pull request. Focus on:
            1. Security vulnerabilities
            2. Performance regressions
            3. Missing error handling
            4. Test coverage
            Post your review as a PR comment.
```

### GitHub Action: Auto-Fix Lint Errors

```yaml
# .github/workflows/claude-fix.yml
name: Claude Auto-Fix
on:
  push:
    branches: [main]

jobs:
  fix:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: anthropics/claude-code-action@v1
        with:
          anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
          prompt: "Run the linter. If there are errors, fix them and commit."
          allowed_tools: "Bash(npm run lint *),Edit,Write,Bash(git *)"
```

### SDK Automation Example

```javascript
import { Claude } from "@anthropic-ai/claude-code";

// Nightly code health check
const claude = new Claude();
const result = await claude.sendMessage(
  "Check for: unused dependencies, circular imports, and functions over 50 lines. " +
  "Output a JSON report.",
  { options: { outputFormat: "json", model: "haiku" } }
);
console.log(JSON.parse(result.text));
```

## IDE Integrations

- [VS Code Extension](https://marketplace.visualstudio.com/items?itemName=anthropics.claude-code) - Official VS Code integration with inline diffs and chat panel.
- [JetBrains Plugin](https://plugins.jetbrains.com/plugin/claude-code) - Official IntelliJ/WebStorm/PyCharm integration.
- [Claude Code Desktop](https://claude.ai/download) - Standalone desktop app with terminal integration.
- [Neovim Plugin (avante.nvim)](https://github.com/yetone/avante.nvim) - Neovim integration supporting Claude as a backend.
- [Cursor](https://cursor.com/) - AI-first code editor with Claude model support.
- [Zed Editor](https://zed.dev/) - High-performance editor with built-in Claude assistant.
- **Terminal-only** - Claude Code works in any terminal — iTerm2, Alacritty, Warp, Kitty, WezTerm, tmux, etc.

## Usage Monitors & Cost Management

### Track Your Spending

```bash
# Check current session cost
# Inside Claude Code:
> /cost

# Set a spending limit in your environment
export ANTHROPIC_MAX_TOKENS=100000  # Limit per session
```

### Cost Optimization Tips

- Use `/model haiku` for simple tasks (code explanations, formatting, small fixes).
- Use `/model sonnet` for everyday coding (default, best balance).
- Use `/model opus` only for complex architecture and multi-file refactors.
- Use `/compact` regularly to keep context small and reduce token usage.
- Use headless mode (`-p`) for batch tasks to avoid interactive overhead.
- Set `--max-turns` in automation to prevent runaway sessions.

### Cost Monitoring Tools

- [Anthropic Console](https://console.anthropic.com/) - Official usage dashboard and billing.
- [LLM Cost Calculator](https://llmpricecheck.com/) - Compare Claude Code costs with other AI coding tools.

## Security & Permissions

### Permission System

Claude Code has a granular permission system to control what actions it can take:

```jsonc
// .claude/settings.json
{
  "permissions": {
    "allow": [
      "Read",
      "Write",
      "Edit",
      "Bash(npm run *)",
      "Bash(npx vitest *)",
      "Bash(git status)",
      "Bash(git diff *)",
      "Bash(git log *)",
      "Bash(git add *)",
      "Bash(git commit *)"
    ],
    "deny": [
      "Bash(rm -rf *)",
      "Bash(curl * | bash)",
      "Bash(wget *)",
      "Bash(git push --force *)",
      "Bash(git reset --hard *)",
      "Bash(chmod 777 *)"
    ]
  }
}
```

### Safety Hook: Block Secrets in Commits

```jsonc
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "command": "if echo \"$CLAUDE_TOOL_INPUT\" | grep -qE 'git (add|commit)' && git diff --cached --name-only | grep -qE '\\.(env|pem|key)$'; then echo 'BLOCKED: Refusing to commit secret files' >&2; exit 1; fi"
      }
    ]
  }
}
```

### Best Practices

- Always use project-level `.claude/settings.json` for team-shared permissions.
- Use deny lists for destructive commands (`rm -rf`, `git push --force`).
- Use `--dangerously-skip-permissions` only in fully trusted, automated pipelines.
- Review Claude's actions during the first few sessions before expanding permissions.
- Use the `PreToolUse` hook to implement custom safety checks.

## Community Projects

> Open source projects built with or for Claude Code.

### Tools & Extensions

- [claude-code-action](https://github.com/anthropics/claude-code-action) - GitHub Action for running Claude Code in CI/CD workflows.
- [ClaudeMD](https://github.com/NicolasGandworkin/ClaudeMD) - VS Code extension for editing and managing CLAUDE.md files.
- [claude-code-tmux](https://github.com/shtse8/claude-code-tmux) - Run multiple Claude Code sessions in tmux panes.
- [claude-code-power-pack](https://github.com/nicobailon/claude-code-power-pack) - Collection of slash commands, hooks, and CLAUDE.md templates.
- [mcpservers.org](https://mcpservers.org/) - Directory and registry of MCP servers.
- [mcp.run](https://mcp.run/) - Run MCP servers in a secure sandbox without local installation.
- [Smithery](https://smithery.ai/) - Package registry for MCP servers with one-click install.

### Frameworks & Libraries

- [MCP TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk) - Build custom MCP servers in TypeScript.
- [MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk) - Build custom MCP servers in Python.
- [FastMCP](https://github.com/jlowin/fastmcp) - High-level Python framework for building MCP servers quickly.
- [mcp-framework](https://github.com/QuantGeekDev/mcp-framework) - TypeScript framework for building MCP servers with decorators.

### Example Projects

- [claude-code-examples](https://github.com/anthropics/anthropic-cookbook/tree/main/claude-code) - Official example projects and patterns from Anthropic.
- [awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) - Curated list of MCP server implementations.

## Articles & Blog Posts

- [Introducing Claude Code](https://www.anthropic.com/news/claude-code) - Official announcement from Anthropic.
- [Claude Code: Best Practices for Agentic Coding](https://www.anthropic.com/engineering/claude-code-best-practices) - Engineering deep-dive from the Anthropic team.
- [How We Build Software at Anthropic](https://www.anthropic.com/engineering/swe-bench-sonnet) - How Anthropic uses Claude Code internally.
- [Claude Code and the Model Context Protocol](https://modelcontextprotocol.io/tutorials/claude-code) - Tutorial on extending Claude Code with MCP.
- [Tips for Using Claude Code Effectively](https://docs.anthropic.com/en/docs/claude-code/tips) - Official tips from Anthropic's docs.
- [Building AI Agents with Claude Code SDK](https://docs.anthropic.com/en/docs/claude-code/sdk) - Guide to building custom agents.
- [Claude Code Hooks Deep Dive](https://docs.anthropic.com/en/docs/claude-code/hooks) - Comprehensive guide to the hooks system.
- [Claude Max and Claude Code](https://www.anthropic.com/news/max-plan) - Using Claude Code with the Max subscription plan.

## Videos & Tutorials

- [Claude Code Official Demo](https://www.youtube.com/watch?v=Oq9oSVL3U3M) - Official Anthropic demo of Claude Code capabilities.
- [Claude Code in 100 Seconds](https://www.youtube.com/watch?v=H_OaCSECbGo) - Fireship's quick overview of Claude Code.

*Know a great video tutorial? [Submit a PR!](CONTRIBUTING.md)*

## Community

- [Claude Code GitHub Discussions](https://github.com/anthropics/claude-code/discussions) - Official community discussions.
- [r/ClaudeAI](https://www.reddit.com/r/ClaudeAI/) - Reddit community for all things Claude.
- [Anthropic Discord](https://discord.gg/anthropic) - Official Anthropic Discord server.
- [Claude Code Twitter/X Community](https://x.com/search?q=%23claudecode) - Follow #claudecode for tips and projects.
- [MCP Discord](https://discord.gg/modelcontextprotocol) - Community for MCP server development.

---

## Contributing

Contributions are welcome! Please read the [contribution guidelines](CONTRIBUTING.md) first.

We especially need:
- **Community projects** — tools, extensions, and integrations you've built.
- **CLAUDE.md templates** — for frameworks not yet covered.
- **Hook recipes** — working examples that solve real problems.
- **Articles & tutorials** — quality content about Claude Code workflows.

## Maintainer

**Erkan** — GitHub: [@erkcet](https://github.com/erkcet)

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the maintainer has waived all copyright and related rights to this work.

---

<details>
<summary>Star History</summary>

[![Star History Chart](https://api.star-history.com/svg?repos=erkcet/awesome-claude-code&type=Date)](https://star-history.com/#erkcet/awesome-claude-code&Date)

</details>
