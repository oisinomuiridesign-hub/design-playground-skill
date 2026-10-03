# Building Design Playgrounds — Claude Skill

Explore design variations of a **real** component without touching production.

The skill has Claude scaffold a hidden `/playground/<feature>` route inside your existing codebase where versions stack non-destructively:

- **`default` mirrors the live component** — it imports the actual production code, never a mock.
- **Every variation is its own component file** (v1, v2, …) — editing one can never break another.
- **Hidden but shipped** — deploys with your app, but `noindex`, excluded from the sitemap, and blocked in `robots.txt`. Reachable only by URL, so you can share a single version with a link.

The payoff: a workbench you come back to months later to steal your own concepts.

Adapted from Ridd's ([@ridd_design](https://x.com/ridd_design)) AI design workflow.

## Install

### Claude Code (plugin marketplace)

```
/plugin marketplace add oisinomuiridesign-hub/design-playground-skill
/plugin install design-playground@oo-design-playground
```

### Manual (Claude Code)

```bash
git clone https://github.com/oisinomuiridesign-hub/design-playground-skill.git
cp -r design-playground-skill/plugins/design-playground/skills/building-design-playgrounds ~/.claude/skills/
```

### claude.ai / Claude Desktop

Zip `plugins/design-playground/skills/building-design-playgrounds/` and upload it under **Settings → Capabilities → Skills**.

## Use

In any web project, ask:

- "Make a playground for the project card on the work page"
- "Scaffold a design playground so I can explore variations of the pricing table"

Claude detects your stack (Next.js, Vite + React Router, Astro, …), builds the shell and version rail first, wires `default` to the production component, then you add versions as you explore.

The skill also includes a copy-paste prompt you can drop into any project directly — see `SKILL.md`.

## License

MIT
