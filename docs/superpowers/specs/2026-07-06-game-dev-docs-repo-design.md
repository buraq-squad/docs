# Game Dev Docs Repo — Design

## Purpose

A central documentation repo for Buraq Squad, covering all disciplines (engineering,
art, design, production) rather than engineers only. Primary goal is onboarding new
hires quickly; secondary goal is serving as an ongoing reference/knowledge base.

## Repo & Hosting

- GitHub repo: `buraq-squad/docs`, **public**.
  - Originally planned as private, but the `buraq-squad` org is on the GitHub Free plan,
    which does not support GitHub Pages for private repositories at all (confirmed via a
    422 from the Pages API: "Your current plan does not support GitHub Pages for this
    repository"). The team chose to make the repo public rather than pay for GitHub Team
    to unlock private-repo Pages. Content is placeholder-only at this stage.
- Static site built with **MkDocs + Material theme** (plain Markdown source, YAML nav
  config — no framework/build complexity, easy for non-engineers to contribute to).
- Deployed to **GitHub Pages** via a GitHub Actions workflow triggered on push to `main`,
  publishing to https://buraq-squad.github.io/docs/.

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
