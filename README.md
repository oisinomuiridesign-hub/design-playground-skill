# Building Design Playgrounds — Claude Skill

Explore design variations of a **real** component without touching production.

The skill has Claude scaffold a hidden `/playground/<feature>` route inside your existing codebase where versions stack non-destructively:

- **`default` mirrors the live component** — it imports the actual production code, never a mock.
- **Every variation is its own component file** (v1, v2, …) — editing one can never break another.
- **Hidden but shipped** — deploys with your app, but `noindex`, excluded from the sitemap, and blocked in `robots.txt`. Reachable only by URL, so you can share a single version with a link.

The payoff: a workbench you come back to months later to steal your own concepts.

Follows the open [Agent Skills](https://agentskills.io) format, so it works in Claude Code, claude.ai, Claude Desktop and other agents that support skills.

Adapted from Ridd's ([@ridd_design](https://x.com/ridd_design)) AI design workflow.

## Install

**Skills CLI (Claude Code, Codex, Cursor, and other agents)**

```bash
npx skills add oisinomuiridesign-hub/design-playground-skill
```

**claude.ai / Claude Desktop**

1. Download `building-design-playgrounds.zip` from the [latest release](https://github.com/oisinomuiridesign-hub/design-playground-skill/releases/latest).
2. Go to **Settings → Capabilities → Skills → Upload skill** and pick the zip.

**Manual (Claude Code)**

```bash
git clone https://github.com/oisinomuiridesign-hub/design-playground-skill.git ~/.claude/skills/building-design-playgrounds
```

## Use

In any web project, ask:

- "Make a playground for the project card on the work page"
- "Scaffold a design playground so I can explore variations of the pricing table"

Claude detects your stack (Next.js, Vite + React Router, Astro, …), builds the shell and version rail first, wires `default` to the production component, then you add versions as you explore.

The skill also includes a copy-paste prompt you can drop into any project directly — see `SKILL.md`.

## License

MIT
