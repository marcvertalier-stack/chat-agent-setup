---
name: "feature-split"
description: "Decides whether a project should be split into features and, if so, produces the feature list (goal, boundary, optional dependencies). Use at the start of a project or when its scope grows, before specifying any feature."
---

# feature-split (v0)

## Purpose

Set the right level of structure before development starts: no needless roadmap for an exploratory prototype, and no unguided development for an application that combines several capabilities.

The skill stops at the boundaries between features. It does not specify a feature in detail and does not break it down into tasks.

## When to use

- At the start of a project, once the goal is known.
- When the scope grows: a new capability appears in a project that was not split, or an existing feature list no longer matches the project.

## Step 1 — Decide: split or not

| Situation | Signals | Decision |
|---|---|---|
| **Exploratory prototype** | A single goal, simple scope, throwaway result or meant for learning ("can the model do X?") | Do not split |
| **Application to split** | Several distinct capabilities you would want to deliver or validate separately, result meant to last | Split |

When in doubt, **do not split**. Come back to this skill as soon as a second distinct capability appears: re-splitting later is cheap, over-planning early costs time and locks in assumptions.

State the decision in one sentence, with the signals that justify it.

## Step 2a — No split

- Restate the overall goal in one or two sentences.
- Write an observable definition of "done".
- Artifacts produced (scripts, notebooks, trial outputs) are throwaway and go in the exploration folder (`explorations/` — name to be confirmed), **never in `tests/`**:
  - tests check code behavior, are durable and run in CI;
  - explorations check a hypothesis, are throwaway and run outside CI.
- When an exploration validates a hypothesis, record its conclusion in a durable artifact. Whatever needs to last then goes through a feature with real tests. Production code never depends on the exploration folder.

The decision and the goal are recorded in `project-memory/feature-split.md` (see Output). No `features/<slug>/` folder is created.

## Step 2b — Split

For each feature:

- **Short name** (slug), used as the folder name `features/<slug>/`.
- **Goal**: the value it delivers, in one sentence.
- **Boundary**: what it includes and what it explicitly excludes.
- **Depends on**: only if a real dependency exists (data, outputs or contracts of another feature). Otherwise, omit.

Splitting rules:

- A feature is a **vertical slice**: it delivers value that is testable end to end. Do not split by technical layer ("backend", "UI", "storage").
- If several features rely on the same foundation (data model, tool contract), make it a separate, explicit feature rather than burying it in the first business feature.
- Order the features: foundation first, then by value and dependencies.
- Do not go down to implementation level.

## Step 3 — Human validation

Present the decision and, if applicable, the list. **Write nothing before validation.** The split is a structural decision that belongs to the human.

## Output

After validation, write `project-memory/feature-split.md`, following the template below. The file is written in both cases:

- **No split**: the decision, its justification, the goal and the definition of "done".
- **Split**: the decision, its justification and the feature list.

The split is project knowledge, not feature work: it lives with the other explicit, versioned project knowledge. Each feature gets its own working folder `features/<slug>/` when work on it starts, not before; this skill does not create it.

The file contains no dates, milestones or scheduling.

### Template

````markdown
# Feature split

<!-- Project knowledge written by the feature-split skill. No dates, milestones or scheduling. -->

Decision: <split | no split> — <one-sentence justification, with the signals observed>

<!-- If no split: keep this section and delete the "Feature list" section. -->
## Goal

- Goal: <overall goal in one or two sentences>
- Done when: <observable definition of "done">

<!-- If split: keep this section and delete the "Goal" section. -->
## Feature list

| # | Feature | Goal | Depends on |
|---|---|---|---|
| 1 | <slug> | <goal> | — |
| 2 | <slug> | <goal> | 1 |

### <slug>

- Goal: …
- Includes: …
- Excludes: …
- Depends on: … (omit if none)
````

## Re-splitting

If `project-memory/feature-split.md` already exists, start from that file, including the justification of the previous decision: propose additions, merges or removals, without rewriting features already delivered.

## Out of scope (v0)

- Detailed feature specification, acceptance criteria, breakdown into tasks: these belong to feature planning.
- Interface contracts fixed upfront between features. To be added as an attribute if a project shows the need, not as a separate case.
- Deterministic check of `project-memory/feature-split.md`.

## Open points

- Name of the exploration folder.
- Owning pack (`project` or Core).