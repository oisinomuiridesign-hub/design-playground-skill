---
name: building-design-playgrounds
description: Use when you want to explore visual/design variations of a real component without touching production — building a hidden, in-repo "playground" route where versions stack non-destructively, the default mirrors the live component, and each variation is a real, shareable artifact. Triggers — "make a playground", "design playground", "explore variations of this component", "scaffold a sandbox for this UI", "stack versions of a component", "self-plagiarize my own concepts later".
---

# Building Design Playgrounds

## Overview

A **playground** is a hidden route inside a production codebase where you explore design variations of a real component. It ships with the app but is invisible to the public — you reach it by knowing the URL. Adapted from Ridd's (ridd_design) AI design workflow.

The point is not "a sandbox page." It's a **workbench you return to months later to steal your own concepts** ("self-plagiarize"). That payoff only exists if three properties hold.

## The Three Load-Bearing Properties

1. **Non-destructive versioning.** The `default` is the immutable source of truth — never edited in place. Duplicating a version creates a *brand-new, independent component file* (v1, v2, …), so editing one can never affect another or the default. Each version is a real, separately-addressable component. On refresh the route resolves to the most recent version.

2. **Hidden but shipped.** The route lives *in* the production codebase and deploys with it, but is undiscoverable: no nav/sitemap links, excluded from sitemap generation, `noindex` (robots meta / `X-Robots-Tag` + `Disallow: /playground` in robots.txt). Findable by URL only — not a separate repo, not Storybook.

3. **Production-fidelity seed.** `default` imports the *actual* production component (match the real code, don't re-create it). Dummy data is pulled from real images/avatars/copy already on the site so explorations stay honest.

If a request drops any of these, it's not a playground — push back.

## Workflow

1. **Detect the stack first.** Inspect router/framework (Next.js app/pages, Vite + React Router, Astro, etc.) and where components/routes live. Adapt the route convention to what's there — never impose a stack.
2. **Scaffold before concepts.** Build the shell, version rail, `default`-from-production import, and the duplicate→new-component mechanism *before* any variation.
3. **Add versions as you explore.** Each new direction = a duplicate = a new component file.
4. **Expose for sharing when ready** (optional): make the route reachable without auth so a plain link works for reviewers.

## The Reusable Prompt

Send this to the target project. Fill the one bracketed line.

```
I want to build a hidden "playground" environment inside this project — a place
where I can explore design variations of a real component, stacked as versions,
that ships with production but is invisible to the public. Build it as reusable
scaffolding, not a one-off page.

FIRST: inspect the repo and tell me the router/framework and where components and
routes live. Adapt everything below to the conventions you find — don't impose a stack.

TARGET FOR THIS FIRST PLAYGROUND:
[ the component I want to explore — e.g. "the project card on the work index page" ]

Rules:
1. ROUTE. Create /playground/<feature> (pick a sensible slug). Structure it so I can
   add more /playground/* routes later by copying the pattern.
2. HIDDEN BUT SHIPPED. Deploys with production but undiscoverable: no nav/sitemap
   links, exclude from sitemap generation, add noindex (robots meta / X-Robots-Tag)
   and Disallow: /playground in robots.txt. I find it by knowing the URL.
3. VERSION RAIL. Left sidebar listing every version. First entry is "default" and
   imports the ACTUAL production component — match its real code exactly, don't recreate it.
4. PRODUCTION-FIDELITY SEED. If default needs dummy data, pull real images/avatars/copy
   already used elsewhere on this site so it feels real.
5. NON-DESTRUCTIVE VERSIONING (core requirement):
   - "default" is the immutable source of truth — NEVER edited in place.
   - Duplicating a version creates a brand-new independent component file (v1, v2, …),
     so editing one version can never affect another or the default.
   - On refresh, the route resolves to the MOST RECENT version.
   - Versions are independently linkable (e.g. ?v=2 or sub-route) so I can share one.
6. SCAFFOLDING FIRST. Build shell + version rail + default-from-production import +
   duplicate-to-new-component mechanism BEFORE any variations.

When done, show me: the route URL, how I add a new version, and confirm the default is
wired to the live component and the route is noindex'd.
```

## Common Mistakes

| Mistake | Fix |
|---|---|
| Versions share one component, edited in place | Each duplicate must be its own file — that's what enables returning later |
| `default` is a hand-built mock | Import the real production component; match its code diff |
| Built as a separate repo / Storybook | It lives in the production codebase, behind a hidden route |
| Forgot noindex / sitemap exclusion | Public or crawlers can find it; add robots meta + robots.txt disallow |
| Built variations before the scaffold | Scaffold the version mechanism first, then explore |
