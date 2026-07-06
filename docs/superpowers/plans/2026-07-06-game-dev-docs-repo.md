# Game Dev Docs Repo Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Scaffold a private MkDocs + Material docs repo for Buraq Squad (`buraq-squad/docs`), covering engineering, art, design, and production, with placeholder pages and a GitHub Pages deploy workflow.

**Architecture:** Plain Markdown content under `docs/`, `mkdocs.yml` driving nav + theme, GitHub Actions building and deploying via `mkdocs gh-deploy` on push to `main`. No "tests" in the traditional sense — verification is `mkdocs build --strict`, which fails the build if `mkdocs.yml` nav references a missing file or a page has a broken internal link.

**Tech Stack:** MkDocs, mkdocs-material, Python 3, GitHub Actions, GitHub Pages.

---

## Reference: full repo layout

```
docs-repo/
├── mkdocs.yml
├── requirements.txt
├── .gitignore
├── README.md
├── .github/workflows/deploy.yml
└── docs/
    ├── index.md
    ├── onboarding/
    │   ├── getting-started.md
    │   ├── team-and-tools.md
    │   └── first-week-checklist.md
    ├── engineering/
    │   ├── godot-conventions.md
    │   ├── git-workflow.md
    │   ├── architecture.md
    │   └── tooling.md
    ├── art/
    │   ├── asset-pipeline.md
    │   ├── import-settings.md
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
        └── how-to-write-docs.md
```

Note: this repo's own working directory (`/Users/shqear/workspace-games/docs`) already has a
`docs/superpowers/specs/` and `docs/superpowers/plans/` folder (this plan lives there). The
MkDocs content above lives in the same `docs/` folder, alongside `docs/superpowers/`. Since
`mkdocs.yml` only lists the nav pages explicitly, the `superpowers/` subfolder is not part of
the built site and does not need excluding — MkDocs only serves what's referenced or found by
directory scan; `docs/superpowers/*.md` files won't be in nav, but MkDocs will still copy them
into the built site as unlisted pages. Task 1 sets `docs_dir` handling explicitly to avoid this
(see Task 1 Step 2).

---

### Task 1: Config scaffolding (mkdocs.yml, requirements.txt, .gitignore, README.md)

**Files:**
- Create: `mkdocs.yml`
- Create: `requirements.txt`
- Create: `.gitignore`
- Create: `README.md`

- [ ] **Step 1: Create `requirements.txt`**

```
mkdocs>=1.6,<2
mkdocs-material>=9.5,<10
```

- [ ] **Step 2: Create `mkdocs.yml`**

Exclude the `superpowers/` planning folder from the built site via `exclude_docs`, and wire
up nav for every content page this plan will create.

```yaml
site_name: Buraq Squad Docs
site_description: Internal documentation for game development at Buraq Squad
docs_dir: docs
site_dir: site

exclude_docs: |
  superpowers/

theme:
  name: material
  palette:
    - scheme: default
      primary: indigo
      toggle:
        icon: material/brightness-7
        name: Switch to dark mode
    - scheme: slate
      primary: indigo
      toggle:
        icon: material/brightness-4
        name: Switch to light mode
  features:
    - navigation.tabs
    - navigation.top
    - search.suggest
    - content.code.copy

nav:
  - Home: index.md
  - Onboarding:
      - Getting Started: onboarding/getting-started.md
      - Team & Tools: onboarding/team-and-tools.md
      - First Week Checklist: onboarding/first-week-checklist.md
  - Engineering:
      - Godot Conventions: engineering/godot-conventions.md
      - Git Workflow: engineering/git-workflow.md
      - Architecture: engineering/architecture.md
      - Tooling: engineering/tooling.md
  - Art:
      - Asset Pipeline: art/asset-pipeline.md
      - Import Settings: art/import-settings.md
      - Naming Conventions: art/naming-conventions.md
  - Design:
      - Game Design Doc Template: design/game-design-doc-template.md
      - Level Design Workflow: design/level-design-workflow.md
      - Scripting for Designers: design/scripting-for-designers.md
  - Production:
      - Bug Reporting: production/bug-reporting.md
      - Build & Release: production/build-and-release.md
      - Milestones & Planning: production/milestones-and-planning.md
  - Contributing:
      - How to Write Docs: contributing/how-to-write-docs.md

markdown_extensions:
  - admonition
  - toc:
      permalink: true
  - pymdownx.highlight
  - pymdownx.superfences
```

- [ ] **Step 3: Create `.gitignore`**

```
site/
.venv/
__pycache__/
*.pyc
.DS_Store
```

- [ ] **Step 4: Create `README.md`**

```markdown
# Buraq Squad Docs

Internal documentation for Buraq Squad game development, covering engineering, art,
design, and production.

## Local preview

\`\`\`bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
\`\`\`

Then open http://127.0.0.1:8000

## Published site

Deployed automatically to GitHub Pages on push to `main`:
https://buraq-squad.github.io/docs/
```

- [ ] **Step 5: Commit**

```bash
git add mkdocs.yml requirements.txt .gitignore README.md
git commit -m "Add MkDocs scaffolding"
```

---

### Task 2: Onboarding pages

**Files:**
- Create: `docs/onboarding/getting-started.md`
- Create: `docs/onboarding/team-and-tools.md`
- Create: `docs/onboarding/first-week-checklist.md`

- [ ] **Step 1: Create `docs/onboarding/getting-started.md`**

```markdown
# Getting Started

<!-- TODO: List required accounts (GitHub org, Slack/Discord, task tracker, Google Workspace, etc.) -->

<!-- TODO: List software to install (Godot version, git, IDE/editor, platform SDKs) -->

<!-- TODO: List repo access steps (which repos to request access to, and from whom) -->
```

- [ ] **Step 2: Create `docs/onboarding/team-and-tools.md`**

```markdown
# Team & Tools

<!-- TODO: Describe team structure (roles, who reports to whom, org chart link) -->

<!-- TODO: List communication tools in use (Slack/Discord channels, meeting cadence) -->

<!-- TODO: List task tracker / project management tool and how to use it -->
```

- [ ] **Step 3: Create `docs/onboarding/first-week-checklist.md`**

```markdown
# First Week Checklist

<!-- TODO: Fill in the concrete first-week checklist items below -->

- [ ] TODO
- [ ] TODO
- [ ] TODO
```

- [ ] **Step 4: Commit**

```bash
git add docs/onboarding
git commit -m "Add onboarding placeholder pages"
```

---

### Task 3: Engineering pages

**Files:**
- Create: `docs/engineering/godot-conventions.md`
- Create: `docs/engineering/git-workflow.md`
- Create: `docs/engineering/architecture.md`
- Create: `docs/engineering/tooling.md`

- [ ] **Step 1: Create `docs/engineering/godot-conventions.md`**

```markdown
# Godot Conventions

<!-- TODO: GDScript style guide (naming, static typing, signals vs direct calls) -->

<!-- TODO: Project/scene folder structure conventions -->

<!-- TODO: Preferred Godot version and how the team keeps it in sync -->
```

- [ ] **Step 2: Create `docs/engineering/git-workflow.md`**

```markdown
# Git Workflow

<!-- TODO: Branching strategy (e.g. trunk-based, feature branches) -->

<!-- TODO: Commit message conventions -->

<!-- TODO: PR/review process and required checks -->
```

- [ ] **Step 3: Create `docs/engineering/architecture.md`**

```markdown
# Architecture

<!-- TODO: High-level overview of core game systems -->

<!-- TODO: Diagrams or links to diagrams of major subsystems -->
```

- [ ] **Step 4: Create `docs/engineering/tooling.md`**

```markdown
# Tooling

<!-- TODO: List of Godot editor plugins/addons used, and why -->

<!-- TODO: List of external tools (build systems, CI, profilers) -->
```

- [ ] **Step 5: Commit**

```bash
git add docs/engineering
git commit -m "Add engineering placeholder pages"
```

---

### Task 4: Art pages

**Files:**
- Create: `docs/art/asset-pipeline.md`
- Create: `docs/art/import-settings.md`
- Create: `docs/art/naming-conventions.md`

- [ ] **Step 1: Create `docs/art/asset-pipeline.md`**

```markdown
# Asset Pipeline

<!-- TODO: Describe the export workflow from DCC tools (e.g. Blender) into Godot -->

<!-- TODO: File formats and folder locations for source vs. imported assets -->
```

- [ ] **Step 2: Create `docs/art/import-settings.md`**

```markdown
# Import Settings

<!-- TODO: Recommended Godot import presets per asset type (textures, models, audio) -->
```

- [ ] **Step 3: Create `docs/art/naming-conventions.md`**

```markdown
# Naming Conventions

<!-- TODO: File and asset naming conventions (case, prefixes, versioning) -->
```

- [ ] **Step 4: Commit**

```bash
git add docs/art
git commit -m "Add art placeholder pages"
```

---

### Task 5: Design pages

**Files:**
- Create: `docs/design/game-design-doc-template.md`
- Create: `docs/design/level-design-workflow.md`
- Create: `docs/design/scripting-for-designers.md`

- [ ] **Step 1: Create `docs/design/game-design-doc-template.md`**

```markdown
# Game Design Doc Template

<!-- TODO: Standard template/sections every game design doc should include -->
```

- [ ] **Step 2: Create `docs/design/level-design-workflow.md`**

```markdown
# Level Design Workflow

<!-- TODO: Steps from concept to playable level -->

<!-- TODO: Tools used for level design (Godot editor, external tools) -->
```

- [ ] **Step 3: Create `docs/design/scripting-for-designers.md`**

```markdown
# Scripting for Designers

<!-- TODO: Basics designers need to know to script simple behavior in Godot -->

<!-- TODO: Links to beginner GDScript resources -->
```

- [ ] **Step 4: Commit**

```bash
git add docs/design
git commit -m "Add design placeholder pages"
```

---

### Task 6: Production pages

**Files:**
- Create: `docs/production/bug-reporting.md`
- Create: `docs/production/build-and-release.md`
- Create: `docs/production/milestones-and-planning.md`

- [ ] **Step 1: Create `docs/production/bug-reporting.md`**

```markdown
# Bug Reporting

<!-- TODO: Where to file bugs (tracker link) and what info reports must include -->
```

- [ ] **Step 2: Create `docs/production/build-and-release.md`**

```markdown
# Build & Release

<!-- TODO: How builds are produced and where they're distributed -->

<!-- TODO: Release checklist -->
```

- [ ] **Step 3: Create `docs/production/milestones-and-planning.md`**

```markdown
# Milestones & Planning

<!-- TODO: How milestones are planned and tracked -->
```

- [ ] **Step 4: Commit**

```bash
git add docs/production
git commit -m "Add production placeholder pages"
```

---

### Task 7: Home page and contributing guide

**Files:**
- Create: `docs/index.md`
- Create: `docs/contributing/how-to-write-docs.md`

- [ ] **Step 1: Create `docs/index.md`**

```markdown
# Welcome to Buraq Squad Docs

This is the internal documentation hub for everyone at Buraq Squad — engineers,
artists, designers, and production.

## How to use these docs

- Browse by discipline in the navigation sidebar.
- Use the search bar (top of page) to find anything quickly.
- If something is missing or wrong, see [How to Write Docs](contributing/how-to-write-docs.md)
  for how to contribute.

## Sections

- **Onboarding** — start here if you're new.
- **Engineering** — Godot conventions, git workflow, architecture.
- **Art** — asset pipeline, import settings, naming conventions.
- **Design** — game design docs, level design workflow.
- **Production** — bug reporting, releases, milestones.

<!-- TODO: Add a short "who we are" blurb and links to key external tools (Slack, task tracker, etc.) -->
```

- [ ] **Step 2: Create `docs/contributing/how-to-write-docs.md`**

```markdown
# How to Write Docs

This repo uses [MkDocs](https://www.mkdocs.org/) with the
[Material theme](https://squidfunk.github.io/mkdocs-material/).

## Adding a page

1. Create a new `.md` file under the relevant section folder in `docs/`.
2. Add it to the `nav:` section in `mkdocs.yml`.
3. Preview locally with `mkdocs serve` before committing.

## Style

- Keep pages focused on one topic.
- Prefer short paragraphs and bullet lists over long prose.
- Use relative links to reference other docs pages.
```

- [ ] **Step 3: Commit**

```bash
git add docs/index.md docs/contributing
git commit -m "Add home page and contributing guide"
```

---

### Task 8: Verify the site builds

**Files:** none (verification only)

- [ ] **Step 1: Create a virtualenv and install dependencies**

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

- [ ] **Step 2: Build in strict mode**

```bash
mkdocs build --strict
```

Expected: exits 0 with no warnings. `--strict` turns nav/link warnings (e.g. a `mkdocs.yml`
nav entry pointing at a file that doesn't exist, or a broken relative link between pages)
into build failures, so a clean exit confirms every page in Tasks 1–7 is wired up correctly.

- [ ] **Step 3: Confirm `docs/superpowers/` was excluded from the build**

```bash
ls site | grep -i superpowers
```

Expected: no output (the folder should not appear under `site/`).

- [ ] **Step 4: Clean up the local build output**

```bash
deactivate
rm -rf site .venv
```

(`site/` and `.venv/` are already in `.gitignore` from Task 1, so this step just keeps the
working tree tidy — nothing to commit here.)

---

### Task 9: GitHub Actions deploy workflow

**Files:**
- Create: `.github/workflows/deploy.yml`

- [ ] **Step 1: Create `.github/workflows/deploy.yml`**

```yaml
name: Deploy docs

on:
  push:
    branches: [main]

permissions:
  contents: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: "3.x"
      - run: pip install -r requirements.txt
      - run: mkdocs gh-deploy --force
```

- [ ] **Step 2: Commit**

```bash
git add .github/workflows/deploy.yml
git commit -m "Add GitHub Pages deploy workflow"
```

---

### Task 10: Create the GitHub repo and push

This task touches shared/remote state (creates a new repo under the `buraq-squad` org and
pushes to it). **Confirm with the user before running these commands** — do not run them
automatically as part of a batch.

**Files:** none (remote setup only)

- [ ] **Step 1: Create the private repo under the org**

```bash
gh repo create buraq-squad/docs --private --source=. --remote=origin
```

Expected: repo created at `https://github.com/buraq-squad/docs`, `origin` remote added
pointing at it.

- [ ] **Step 2: Push `main`**

```bash
git push -u origin main
```

Expected: `main` branch pushed, upstream tracking set.

- [ ] **Step 3: Enable GitHub Pages for the `gh-pages` branch**

After the first push to `main`, the deploy workflow (Task 9) runs automatically and creates
a `gh-pages` branch via `mkdocs gh-deploy`. Once that branch exists:

```bash
gh api repos/buraq-squad/docs/pages -X POST -f source[branch]=gh-pages -f source[path]=/
```

Expected: Pages enabled, site published at `https://buraq-squad.github.io/docs/`.

- [ ] **Step 4: Verify the deploy workflow ran successfully**

```bash
gh run list --repo buraq-squad/docs --limit 1
```

Expected: most recent run for `Deploy docs` shows status `completed` / conclusion `success`.

---

## Plan Self-Review Notes

- **Spec coverage:** all sections from the design doc (repo/hosting, content structure by
  discipline, supporting files) map to Tasks 1–9; Task 10 covers the remote repo/Pages setup
  called out in the design's Hosting section.
- **Nav/file consistency:** every path listed in `mkdocs.yml`'s `nav` (Task 1) is created by
  Tasks 2–7 with matching paths; Task 8 verifies this with `mkdocs build --strict` rather than
  relying on manual cross-checking.
- **Out of scope reminder:** per the design doc, this plan does not author real content beyond
  placeholders, does not attempt Enterprise-only Pages access control, and does not add
  versioning.
