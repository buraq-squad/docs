# Build & Release

We use [release-please](https://github.com/googleapis/release-please) to
turn merged work on `main` into versioned, changelogged releases, and a
tag-triggered workflow to actually build and publish from those releases.

<!-- TODO: fill in per-project distribution targets (itch.io, Play Console
     internal track, Steam, App Store) and where their secrets/credentials
     live -->

## Why release-please

Release-please reads [Conventional Commits](https://www.conventionalcommits.org/)
on `main` and keeps a standing **release PR** up to date with the next
version bump and changelog, computed from those commits. Merging that PR
tags the release (e.g. `v1.4.0`) and updates `CHANGELOG.md` — nobody hand-
writes a changelog or decides the version number by hand.

It solves version bumping and changelog generation. It does **not** build
anything — a separate workflow, triggered by the tag it creates, is
responsible for producing and publishing the actual build.

## Commit convention

Release-please only sees what your commit messages tell it, so PR titles
(squash-merge commit messages) must follow Conventional Commits:

| Prefix              | Effect                          |
| -------------------- | -------------------------------|
| `fix: ...`            | Patch bump (`1.2.0` → `1.2.1`) |
| `feat: ...`           | Minor bump (`1.2.0` → `1.3.0`) |
| `feat!: ...` / `BREAKING CHANGE:` footer | Major bump (`1.2.0` → `2.0.0`) |
| `chore:`, `docs:`, `style:`, `refactor:`, `test:` | No version bump, but still logged |

A commit that doesn't follow this format is invisible to release-please —
it won't trigger a bump or show up in the changelog. Use scopes where
useful, e.g. `fix(pdf): ...`, `feat(inventory): ...`.

## The two-stage pipeline

1. **Release-please workflow** — runs on every push to `main`. Opens or
   updates a `chore(main): release X.Y.Z` PR containing the version bump
   and changelog. Merging that PR creates the `vX.Y.Z` tag.
2. **Build & publish workflow** — triggers on that `v*` tag push. Builds
   the real artifact and pushes it to its distribution target.

Keeping these as two separate workflows means the release PR can sit
un-merged (for review, or to batch several fixes into one release)
without ever triggering a build.

## Godot projects

For Godot projects, configure release-please's `extra-files` to bump
`config/version` in `project.godot` alongside its usual version file, so
the in-game build number always matches the git tag:

```json
{
  "extra-files": [
    { "type": "generic", "path": "project.godot" }
  ]
}
```

The build workflow (triggered by the tag) then runs the Godot export
templates for each target platform and uploads the result.

<!-- TODO: link the actual export/build workflow once it exists per project -->

## When this doesn't apply

Release-please assumes iterative, versioned releases. It's a good fit for:

- Live games and services taking regular post-launch updates (e.g. the
  Android mini-games).
- Backend services and internal tools.

It's a poor fit for a single milestone ship (a game going Gold once) —
semver and auto-changelog add little when there's no ongoing release
cadence. For those, track builds against the
[milestone plan](milestones-and-planning.md) instead, and only adopt
release-please once the game is live and iterating.

## Release checklist

- [ ] All sprint work targeted for this release is `Done` in
      [Plane](using-plane.md) and merged to `main`.
- [ ] The release-please PR's changelog looks correct — no missing or
      mis-categorized entries.
- [ ] Merge the release-please PR.
- [ ] Confirm the build/publish workflow triggered by the new tag
      succeeded.
- [ ] Smoke-test the published build before announcing.
