# Milestones & Planning

We use an Agile workflow adapted for game development: short sprints for
day-to-day execution, wrapped by longer production milestones that track
the overall shape of the game.

## Why Agile for games

Game development has more unknowns than typical software work — fun isn't
always predictable, and scope changes as prototypes prove out (or don't).
Agile gives us short feedback loops so we catch a bad design direction in
weeks, not months, while milestones keep the team aligned on the bigger
picture the sprints are building toward.

## Roles

- **Producer** — owns the roadmap and milestone plan, runs planning and
  review meetings, clears blockers.
- **Discipline leads** (design, engineering, art) — own their backlog,
  break down work into sprint-sized tasks, represent their discipline in
  planning.
- **Team members** — pick up tasks, keep their board status current,
  flag blockers as soon as they appear rather than at standup.

## Sprints

- **Length:** 2 weeks.
- **Sprint planning:** first day of the sprint. Each discipline pulls
  tasks from its backlog into the sprint based on priority and capacity.
- **Daily standup:** 15 minutes, async-friendly. Each person shares what
  they did, what they're doing next, and any blockers.
- **Sprint review:** last day of the sprint. Play the build. Anything not
  actually playable/working doesn't count as done.
- **Retro:** immediately after review. What worked, what didn't, one or
  two concrete changes to try next sprint.

## Backlog

- Tracked in the task tracker (see [Team & Tools](../onboarding/team-and-tools.md)).
- Each item has: a clear one-line description, an owner's discipline, a
  size estimate, and a link to the relevant design doc or spec if one
  exists.
- Leads groom their backlog weekly — reprioritize, split anything too big
  for one sprint, close anything that's no longer relevant.

## Definition of done

A task is done when it's:

- Implemented and merged (or placed and tested, for content tasks).
- Playable in the current build — not just "code complete."
- Free of known regressions in adjacent systems.

Anything that doesn't meet this bar stays in progress and rolls into the
next sprint rather than being marked done.

## Milestones

Sprints roll up into production milestones, which are the checkpoints we
use to judge whether the game is on track:

| Milestone      | Goal                                                              |
| -------------- | ------------------------------------------------------------------|
| Prototype      | Core loop is fun in isolation, on paper mechanics, no real content |
| Vertical Slice | One full slice (art, audio, UI, gameplay) at target quality        |
| Alpha          | Feature complete — all systems exist, content still incomplete     |
| Beta           | Content complete — polish, balancing, and bug fixing only          |
| Gold           | Shippable build                                                    |

Each milestone has its own review: play the build against the milestone's
goal, decide go/no-go on scope for the next phase, and adjust the roadmap
if needed. See [Build & Release](build-and-release.md) for how milestone
builds are cut.

## Scope changes

Scope creep is the biggest risk to any milestone. If new work comes up
mid-sprint:

- It goes into the backlog, not directly into the current sprint.
- The producer and relevant lead decide whether it's urgent enough to
  swap for something already committed — swapping in without swapping
  something out isn't allowed.
