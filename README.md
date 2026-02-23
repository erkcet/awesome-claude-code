# Awesome Claude Code [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of resources, tools, tips, and community projects for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) — Anthropic's official CLI for Claude.

Claude Code is an agentic coding tool that lives in your terminal, understands your codebase, and helps you code faster through natural language commands. This list aims to be the definitive community resource for everything Claude Code.

**Contributions welcome!** Read the [contribution guidelines](CONTRIBUTING.md) before submitting a PR.

---

## Contents

- [Official Resources](#official-resources)
- [Getting Started](#getting-started)
- [CLAUDE.md Templates](#claudemd-templates)
- [MCP Servers](#mcp-servers)
- [Hooks](#hooks)
- [Workflows & Patterns](#workflows--patterns)
- [IDE Integrations](#ide-integrations)
- [Custom Slash Commands](#custom-slash-commands)
- [Tips & Tricks](#tips--tricks)
- [Context Management](#context-management)
- [CLI Usage](#cli-usage)
- [Community Projects](#community-projects)
- [Articles & Blog Posts](#articles--blog-posts)
- [Videos & Tutorials](#videos--tutorials)
- [Community](#community)

---

## Official Resources

- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code) - Official Anthropic docs.
- [Claude Code GitHub](https://github.com/anthropics/claude-code) - Official repo, issue tracker, and discussions.
- [Anthropic Cookbook](https://github.com/anthropics/anthropic-cookbook) - Official examples and guides from Anthropic.
- [Claude Code Best Practices](https://docs.anthropic.com/en/docs/claude-code/best-practices) - Anthropic's recommended patterns.
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) - Official MCP specification and docs.
- [Claude API Reference](https://docs.anthropic.com/en/api) - Underlying API that powers Claude Code.

## Getting Started

- [Installation Guide](https://docs.anthropic.com/en/docs/claude-code/getting-started) - Official installation and setup instructions.
- [Claude Code Quickstart](https://docs.anthropic.com/en/docs/claude-code/quickstart) - Get up and running in minutes.
- [First Session Walkthrough](https://docs.anthropic.com/en/docs/claude-code/tutorials) - Step-by-step tutorial for your first coding session.

## CLAUDE.md Templates

> `CLAUDE.md` is the memory file Claude Code reads at session start. A good one dramatically improves output quality.

- [Monorepo Template](templates/claudemd/monorepo.md) - For large monorepos with multiple packages.
- [Python Project Template](templates/claudemd/python.md) - Python projects with venv, pytest, linting.
- [TypeScript/Node Template](templates/claudemd/typescript-node.md) - Node.js/TypeScript with npm/pnpm, ESLint, Vitest.
- [React/Next.js Template](templates/claudemd/react-nextjs.md) - Frontend projects with component libraries.
- [Rust Project Template](templates/claudemd/rust.md) - Cargo-based Rust projects.
- [Go Project Template](templates/claudemd/go.md) - Go modules with standard project layout.
- [Homelab/Infrastructure Template](templates/claudemd/homelab.md) - For managing servers, services, and infrastructure.
- [Mobile App Template](templates/claudemd/mobile.md) - React Native / Flutter projects.

### CLAUDE.md Best Practices

- Keep it under 500 lines — Claude reads it every session, so conciseness matters.
- Put the most important context (build commands, architecture) at the top.
- Use tables for structured data (services, ports, API keys).
- Include common commands the bot should know how to run.
- Use nested `CLAUDE.md` files in subdirectories for package-specific context.
- Update it after every significant change to your project.

## MCP Servers

> MCP (Model Context Protocol) servers extend Claude Code with external tools and data sources.

### Official / First-Party

- [mcp-server-filesystem](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem) - Secure file system access with configurable permissions.
- [mcp-server-github](https://github.com/modelcontextprotocol/servers/tree/main/src/github) - GitHub API integration for repos, issues, PRs.
- [mcp-server-postgres](https://github.com/modelcontextprotocol/servers/tree/main/src/postgres) - Read-only PostgreSQL database access.
- [mcp-server-sqlite](https://github.com/modelcontextprotocol/servers/tree/main/src/sqlite) - SQLite database interaction.
- [mcp-server-brave-search](https://github.com/modelcontextprotocol/servers/tree/main/src/brave-search) - Web search via Brave Search API.
- [mcp-server-puppeteer](https://github.com/modelcontextprotocol/servers/tree/main/src/puppeteer) - Browser automation and web scraping.
- [mcp-server-slack](https://github.com/modelcontextprotocol/servers/tree/main/src/slack) - Slack workspace integration.
- [mcp-server-memory](https://github.com/modelcontextprotocol/servers/tree/main/src/memory) - Persistent memory using a knowledge graph.

### Community MCP Servers

- [mcp-server-docker](https://github.com/ckreiling/mcp-server-docker) - Manage Docker containers and images.
- [mcp-server-kubernetes](https://github.com/strowk/mcp-k8s-go) - Kubernetes cluster management.
- [mcp-server-linear](https://github.com/jerhadf/linear-mcp-server) - Linear issue tracker integration.
- [mcp-server-notion](https://github.com/v-3/notion-server) - Notion workspace access.
- [mcp-server-raycast](https://github.com/raycast/mcp-server-raycast) - Raycast integration for macOS.
- [mcp-server-obsidian](https://github.com/smithery-ai/mcp-obsidian) - Obsidian vault access.

## Hooks

> Hooks are shell commands that execute automatically in response to Claude Code events.

### Hook Examples

```jsonc
// .claude/settings.json
{
  "hooks": {
    // Run linter after every file edit
    "post-tool-use": [
      {
        "matcher": "Edit|Write",
        "command": "eslint --fix $CLAUDE_FILE_PATH"
      }
    ],
    // Notify on task completion
    "post-message": [
      {
        "command": "terminal-notifier -message 'Claude finished' -title 'Claude Code'"
      }
    ],
    // Auto-format Python files after edit
    "post-tool-use": [
      {
        "matcher": "Edit|Write",
        "command": "black $CLAUDE_FILE_PATH 2>/dev/null || true"
      }
    ]
  }
}
```

### Hook Use Cases

- Auto-formatting code after edits (Prettier, Black, gofmt).
- Running type checks after file modifications.
- Sending desktop notifications when long tasks complete.
- Auto-committing after successful test runs.
- Logging all tool usage for auditing.
- Triggering CI/CD pipelines on specific actions.

## Workflows & Patterns

### Plan Mode

Use plan mode for non-trivial tasks. It forces Claude to explore the codebase and design an approach before writing code.

```
> /plan Refactor the authentication module to use JWT instead of sessions
```

### Multi-Agent with Worktrees

Use git worktrees for parallel, isolated work:

```
> Work on the login page redesign in a worktree
> # Claude creates an isolated copy — your main branch stays clean
```

### Effective Prompting Patterns

- **Be specific about scope**: "Fix the null check in `src/auth/login.ts:45`" > "Fix the login bug"
- **Reference files directly**: "Read `package.json` and update all outdated deps"
- **Chain tasks**: "Run the tests, fix any failures, then run them again"
- **Set constraints**: "Refactor this function but don't change the public API"
- **Ask for exploration first**: "What files handle payment processing?" before "Refactor payments"

### Git Workflow

```
> /commit                    # Smart commit with conventional message
> Create a PR for this branch # Generates title, description, test plan
```

## IDE Integrations

- [VS Code Extension](https://marketplace.visualstudio.com/items?itemName=anthropics.claude-code) - Official VS Code integration.
- [JetBrains Plugin](https://plugins.jetbrains.com/plugin/claude-code) - Official IntelliJ/WebStorm/PyCharm integration.
- **Terminal-only** - Claude Code works in any terminal — iTerm2, Alacritty, Warp, Kitty, tmux, etc.

## Custom Slash Commands

> Place `.md` files in `.claude/commands/` to create project-specific commands.

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
```

## Tips & Tricks

### Performance

- Use `/compact` to compress conversation history when context gets large.
- Use Haiku model for quick, simple tasks: `--model haiku` or `/model haiku`.
- Use Opus for complex architectural decisions and multi-file refactors.
- Add `--no-permissions` in trusted projects to skip approval prompts (use carefully).

### Productivity

- Use `claude -p "query"` for one-shot questions without entering interactive mode.
- Pipe input: `cat error.log | claude -p "explain this error"`.
- Use `claude --resume` to continue your last conversation.
- Add project-specific commands in `.claude/commands/` for repeated workflows.
- Use `/init` to auto-generate a `CLAUDE.md` for a new project.

### Keybindings

- `Esc` - Cancel current generation.
- `Tab` - Accept autocomplete suggestion.
- Customize keybindings in `~/.claude/keybindings.json`.

## Context Management

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
│   ├── commands/          # Custom slash commands
│   │   ├── review.md
│   │   └── deploy-check.md
│   └── keybindings.json   # Custom keybindings
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

## CLI Usage

### Essential Commands

```bash
# Start interactive session
claude

# One-shot query
claude -p "What does the main function in src/index.ts do?"

# Resume last conversation
claude --resume

# Pipe input
git diff | claude -p "Review these changes"
cat error.log | claude -p "What went wrong?"

# Use specific model
claude --model opus
claude --model sonnet
claude --model haiku

# Initialize CLAUDE.md for a project
claude /init
```

### Useful Piping Patterns

```bash
# Review PR diff
gh pr diff 123 | claude -p "Review this PR for bugs"

# Explain test failures
npm test 2>&1 | claude -p "Why are these tests failing?"

# Analyze logs
tail -100 /var/log/app.log | claude -p "Any errors or warnings?"

# Generate commit message
git diff --staged | claude -p "Write a conventional commit message"
```

## Community Projects

> Open source projects built with or for Claude Code.

*This section is looking for contributions! Submit a PR to add your project.*

## Articles & Blog Posts

- [Introducing Claude Code](https://www.anthropic.com/news/claude-code) - Official announcement from Anthropic.
- [Claude Code: Best practices for agentic coding](https://www.anthropic.com/engineering/claude-code-best-practices) - Anthropic engineering blog.

*Know a great article? Submit a PR!*

## Videos & Tutorials

*This section is looking for contributions! Submit a PR to add your tutorial.*

## Community

- [Claude Code GitHub Discussions](https://github.com/anthropics/claude-code/discussions) - Official community discussions.
- [r/ClaudeAI](https://www.reddit.com/r/ClaudeAI/) - Reddit community for all things Claude.
- [Anthropic Discord](https://discord.gg/anthropic) - Official Anthropic Discord server.

---

## Contributing

Contributions are welcome! Please read the [contribution guidelines](CONTRIBUTING.md) first.

## Maintainer

**Erkan**

- GitHub: [@erkcet](https://github.com/erkcet)

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the maintainer has waived all copyright and related rights to this work.
