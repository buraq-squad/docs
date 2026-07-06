# Game Dev Docs Repo — Design

## Purpose

A central documentation repo for Buraq Squad, covering all disciplines (engineering,
art, design, production) rather than engineers only. Primary goal is onboarding new
hires quickly; secondary goal is serving as an ongoing reference/knowledge base.

## Repo & Hosting

- New GitHub repo: `buraq-squad/docs`, **private**.
- Static site built with **MkDocs + Material theme** (plain Markdown source, YAML nav
  config — no framework/build complexity, easy for non-engineers to contribute to).
- Deployed to **GitHub Pages** via a GitHub Actions workflow triggered on push to `main`.
  - Caveat accepted by the team: GitHub Pages built from a private repo on
    Free/Pro/Team plans produces a site that is technically reachable by anyone with
    the URL, even though the source repo itself stays private and access-controlled.
    True org-only Pages access control requires GitHub Enterprise Cloud, which is not
    in scope now.

## Content Structure

Organized by discipline since the audience spans the whole studio, not just
programmers:

```
docs/
├── index.md                      # Welcome, how to use these docs, how to contribute
├── onboarding/
│   ├── getting-started.md        # Accounts, installs, repo/tool access
│   ├── team-and-tools.md         # Team structure, communication tools, task tracker
│   └── first-week-checklist.md
├── engineering/
│   ├── godot-conventions.md      # GDScript style guide, project/scene structure
│   ├── git-workflow.md           # Branching, commits, PR process
│   ├── architecture.md           # High-level systems overview
│   └── tooling.md                # Editor plugins/addons in use
├── art/
│   ├── asset-pipeline.md         # Export/import workflow
│   ├── import-settings.md        # Godot import presets per asset type
│   └── naming-conventions.md
├── design/
│   ├── game-design-doc-template.md
│   ├── level-design-workflow.md
│   └── scripting-for-designers.md
├── production/
│   ├── bug-reporting.md
│   ├── build-and-release.md
│   └── milestones-and-planning.md
└── contributing/
    └── how-to-write-docs.md      # Style guide for writing/editing these docs
```

Each page ships with a heading structure and placeholder/TODO prompts describing what
should go there — not filled-in content. Team members fill in real content over time.

## Supporting Files

- `mkdocs.yml` — Material theme config, nav matching the structure above, search enabled.
- `.github/workflows/deploy.yml` — on push to `main`: install MkDocs + Material,
  `mkdocs build`, deploy `site/` to the `gh-pages` branch (or Pages deployment action).
- `.gitignore` — Python/MkDocs build artifacts (`site/`, `__pycache__/`, etc.)
- `requirements.txt` — pins `mkdocs` and `mkdocs-material` versions.
- Root `README.md` — short pointer to the published docs site + local preview instructions
  (`mkdocs serve`).

## Out of Scope (for this pass)

- Actual authored content beyond placeholders/TODOs.
- Enterprise-grade access control for the published site.
- Versioned docs per game release (not needed — single evolving knowledge base).
