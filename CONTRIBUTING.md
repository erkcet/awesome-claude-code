# Contributing to Awesome Claude Code

Thanks for your interest in contributing! This list is community-driven, and every contribution helps make it the best resource for Claude Code users.

## What We Need

| Category | Priority | Examples |
|----------|----------|---------|
| Community projects | High | Tools, CLIs, extensions built for Claude Code |
| CLAUDE.md templates | High | Frameworks not yet covered (Elixir, C#/.NET, Vue, etc.) |
| Hook recipes | High | Working hooks that solve real problems |
| Articles & tutorials | Medium | Blog posts, guides, walkthroughs |
| MCP servers | Medium | Community-built MCP server implementations |
| Videos | Low | Video tutorials, demos, conference talks |
| Workflow patterns | Low | Effective prompting strategies, automation scripts |

## Quality Criteria

To keep this list useful and trustworthy, submissions must meet these standards:

### For Projects & Tools
- **Active and maintained** — recent commits within the last 6 months, or stable/feature-complete.
- **100+ GitHub stars OR unique use case** — popular projects are welcome, but niche tools that solve specific problems are too.
- **Working and installable** — must have clear setup instructions and actually work.
- **No spam or low-effort forks** — original work or significant improvements only.

### For Articles & Tutorials
- **Substantive content** — not just "I tried Claude Code and it's cool". Should teach something.
- **Accurate and up-to-date** — outdated articles with deprecated commands will be removed.
- **English language** — all content must be in English.

### For CLAUDE.md Templates
- **Practical over theoretical** — based on real projects, not hypothetical structures.
- **Follow the established format** — Project Overview, Commands table, Project Structure tree, Conventions, Environment Variables, Known Issues.
- **Include explanatory comments** — help users understand and customize.

## How to Contribute

### Adding a Resource

1. Fork this repo.
2. Create a branch: `git checkout -b add-resource-name`.
3. Add your resource to the appropriate section in `README.md`.
4. Submit a pull request.

### Formatting Rules

Follow the existing format exactly:

```markdown
- [Resource Name](https://link.to/resource) - One-line description ending with a period.
```

- Use title case for resource names.
- Descriptions: one sentence, starting with a capital letter, ending with a period.
- Keep descriptions under 120 characters.
- Place new entries at the **end** of the relevant section.
- No star count badges or download stats on entries.

### Submitting a CLAUDE.md Template

1. Place it in `templates/claudemd/`.
2. Name it after the framework/stack (e.g., `django.md`, `svelte.md`).
3. Include the standard header: `# CLAUDE.md — [Framework] Template`.
4. Include all standard sections (see existing templates for reference).
5. Include comments explaining each section.

### Reporting Issues

- **Broken link?** [Open an issue](../../issues/new?template=broken-link.yml) or submit a PR to fix/remove it.
- **Outdated resource?** Open an issue describing what's changed.
- **Suggestion?** [Open a resource suggestion](../../issues/new?template=add-resource.yml).

## Link Validation

All links are automatically checked weekly via GitHub Actions. If a link is reported broken:

1. We'll try to find an updated URL.
2. If the resource is gone, it will be removed.
3. Archived/read-only repos are acceptable if the content is still valuable.

## Removals

Resources may be removed if they:
- Have a broken link that can't be fixed.
- Are abandoned with no activity for 12+ months and no longer work.
- Are superseded by a better alternative.
- Violate our quality criteria.

## Code of Conduct

Be respectful. This is a community resource. Unhelpful, rude, or spammy contributions will be closed without merge.
