---
name: "status-brief"
description: "Produces a 'where do I stand' brief across the user's ongoing workstreams (projects, open chats, repos): last known state, next step, blockers, and what looks stale. Use whenever the user asks 'où en est-on', 'where am I', 'what's the status of my projects/chats', 'qu'est-ce qui est en cours', says they lost track of their parallel conversations, or wants a status check before deciding what to work on. Also the right skill for a recurring (e.g. morning) progress digest of projects and chats. NOT the morning brief (agenda, mail, chat messages): this one tracks progress on workstreams, not the day's schedule."
---

# status-brief (v0 draft)

## Purpose

The user opens many chats in parallel and ends up not knowing where each workstream stands. This skill rebuilds that picture in one short page: for each workstream, what state it is in, what the next step is, and what is blocked. It reports; it does not decide what to do next (that is `topic-dispatch`) and it does not split conversations (that is `topic-split`).

It is distinct from `morning`, which covers agenda, mail and chat messages. If the user wants both, run `morning` for the day and this skill for the workstreams; never merge their logic.

## When to use

- On demand: "où en est-on ?", "fais-moi le point", "status of my projects".
- As a scheduled digest (see "Scheduled mode").
- Standalone by design: it does not need `topic-split` or `topic-dispatch` to have run. It only reads what they leave behind (backlog items, in `backlog.md` and Mem0).

## Step 1 — Gather (all sources are optional; use what exists)

Default is to combine all of them (memory notes, Mem0, chats, git), because notes say what was intended and git says what actually happened. If they disagree, report the disagreement; that is often the most useful line of the brief.

1. **Project notes in memory**: list the memory store, read the `/areas/*.md` files and the project-scoped `areas/` files. These hold decisions, constraints, deadlines and status as the user stated them. Use the file's own wording; do not upgrade a plan into a fact.
2. **Mem0**: if the Mem0 tools exist, page through memories (`get_memories`) and run targeted `search_memories` queries ("next step", "blocked", "decision", the workstream names found in step 1). Entries carry an `app_id` (the project, e.g. `job-hunt-agent`, `data-projects-utils`), a `metadata.type` (`contexte`, `decisions`, and `backlog` if topic-dispatch parked items there) and dates. Group by `app_id` = workstream, use `updated_at` for freshness, and treat `backlog` entries as parked items to list separately. Mem0 holds project context written from Claude Code sessions, so it often knows the real last step where the notes do not. When a Mem0 `app_id` and a memory-note file refer to the same project (use aliases), merge them into one entry.
3. **Recent chats**: if a chat-history tool exists (`recent_chats`, `conversation_search`), pull the last ~7–14 days, group chats by workstream, and note for each: last topic, whether it ended on an open question, and the date. If no such tool is available in this session, say so in one line and continue; do not invent chats.
4. **Backlog file**: if a `backlog.md` is reachable (usually in the `chat-agent-skills` repo, see `topic-dispatch`), read its "Open" section and list those items in a separate "Backlog" block with their age. It is the readable source of truth; Mem0 `backlog` entries are its mirror, so do not list the same item twice, and flag any item present in only one of the two.
5. **Git repositories**: if a shell with access to the user's repos exists, for each repo of a workstream read `git status --short`, `git log -5 --format='%ad %s' --date=short`, open branches and (if `gh` works) open PRs/issues. If repos are not reachable (typical in a cloud run), say "repos not checked" instead of guessing.

Read-only throughout. Never commit, push, edit memory or modify a repo from this skill.

## Step 2 — Build the workstream list

One entry per workstream, not per chat. Merge chats and repos that belong to the same subject (use the `aliases` in memory files). Per entry:

- **State**: one sentence, dated (e.g. "repo not created yet, topic-split drafted — 12 Oct").
- **Next step**: the single most concrete next action, or "unknown" if no source says.
- **Blocked by**: a decision the user owes, a missing access, another workstream. Omit if none.
- **Freshness**: days since last activity from the best source; flag as *stale* beyond ~7 days with an open next step.
- **Sources**: which of notes / Mem0 / chats / git back this entry, so the user can judge confidence.

Only include a fact if a source states it. Mark inferences as such.

## Step 3 — Present

Lead with a 2–3 line headline: how many workstreams, how many blocked, how many stale. Then the list, ordered by need for attention (blocked first, then stale-with-next-step, then healthy). Finish with an "Open questions for you" list of the decisions that block others, at most five.

Keep it a page. The brief is a glance, not an audit. Write in the user's language (French by default for this user).

## Scheduled mode

When the run is unattended (scheduled task), nobody can answer questions: proceed with defaults, state assumptions at the top, and only notify the user if something needs them (a blocked workstream, a stale item with a deadline, a source that could not be read). A brief where nothing changed since the previous run is not worth a notification.

To set it up, use the scheduled-task tools (not local cron), with a standalone prompt that names this skill, the language, and the sources to use. Suggested cadence: weekday mornings. Do this only when the user asks for it.

## Handoff

If the brief reveals a chat that mixes several topics, suggest `topic-split` (the entry point of the other pipeline). Suggest, do not run it uninvited.

## Out of scope

- Prioritizing or scheduling work (`topic-dispatch`).
- Agenda, mail, chat messages (`morning`).
- Writing to memory or repos.

## Open points

- Which source wins when they disagree (default: report the disagreement, no winner).
- Where the user wants the output to live (chat only by default; a doc or artifact only if asked).
