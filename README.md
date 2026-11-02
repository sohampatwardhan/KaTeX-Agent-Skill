# katex — Agent Skill

An [Agent Skill](https://agentskills.io) that serves as a reference for AI coding agents (Claude Code, and any tool that supports the SKILL.md format) to **write and format mathematical expressions that render correctly in KaTeX viewers** — GitHub Markdown/READMEs, Joplin, GitLab, Jupyter, Notion, and VS Code preview.

## Why

KaTeX renders a *subset* of LaTeX, and each host (GitHub, Joplin, …) only enables certain delimiters. Math that compiles in a full LaTeX document often fails silently or shows a red error in a KaTeX viewer. This skill gives agents:

- The correct **delimiters per host** (`$...$`, `$$...$$`, ```` ```math ````) and why `\( \)` / `\[ \]` don't work.
- The **dollar-sign rules** that cause most broken output (escaping `\$`, no interior spaces, blank lines around blocks, keeping `&` raw).
- Copy-paste **quick-reference patterns** for common math (fractions, matrices, cases, aligned derivations, sets, operators).
- The list of LaTeX commands **KaTeX does NOT support**, with substitutions.

## Contents

| File | Purpose |
|------|---------|
| `SKILL.md` | Main reference: delimiters, dollar-sign rules, quick-reference patterns, common mistakes. |
| `references/support-table.md` | Full curated list of supported functions/symbols/environments and the commands KaTeX rejects. |

## Install

### With the `skills` CLI

Install with the [`skills` CLI](https://github.com/vercel-labs/skills) (Node.js 22.20 or later). It records the source, so `npx skills update` keeps the skill current:

```bash
# Global install for every agent the CLI detects
npx skills add sohampatwardhan/KaTeX-Agent-Skill -g

# Or only for chosen agents
npx skills add sohampatwardhan/KaTeX-Agent-Skill -g -a claude-code -a codex

# Update later
npx skills update -g
```

### By hand (Claude Code)

Clone into your personal skills directory (or symlink it):

```bash
git clone https://github.com/sohampatwardhan/KaTeX-Agent-Skill.git ~/.claude/skills/katex
# or, to keep the repo elsewhere and symlink:
ln -s /path/to/KaTeX-Agent-Skill ~/.claude/skills/katex
```

The skill is discovered automatically by its `description` frontmatter whenever you ask an agent to write or format math for a KaTeX viewer. Other agent runtimes recognize `~/.agents/skills/` as a cross-runtime location.

## Versioning

Every `SKILL.md` carries a [SemVer 2.0.0](https://semver.org) version in its frontmatter `metadata` map (`version: "1.0.0"`, quoted). Bump it on any change to the skill:

- **PATCH** for wording tweaks and fixes.
- **MINOR** for new guidance or changed behaviour.
- **MAJOR** for breaking changes, such as renames or removed steps.

CI runs `node scripts/check-skill-versions.mjs`, which fails if any `SKILL.md` is missing `metadata.version` or the value isn't valid SemVer.

## Sources

Built against the official KaTeX documentation:
- <https://katex.org/docs/supported>
- <https://katex.org/docs/support_table>
- <https://github.com/KaTeX/KaTeX/wiki/Things-that-KaTeX-does-not-(yet)-support>

## License

MIT
