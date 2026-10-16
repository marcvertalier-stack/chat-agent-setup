---
name: "topic-dispatch"
description: "Decides what to do with each topic once a conversation has been split into topics: prioritize them, then for each one either prepare a self-contained starter message for a dedicated new conversation (now) or schedule a task for later, and output a clear processing order with 'now' vs 'deferred'. Use right after topic-split, or whenever the user has several parallel topics/chats and says 'dans quel ordre je traite ça', 'what do I do first', 'trie ces sujets', 'ouvre une conversation pour chacun', 'programme ça pour plus tard', or feels overloaded by too many open threads."
---

# topic-dispatch

## Purpose

`topic-split` finds the independent topics in a conversation. This skill decides what happens to each. The user cannot work on everything at once, so the value is the triage: a short ordered list, a few things started now, the rest parked safely with a trigger to come back.

## Input

A list of topics, normally the output of `topic-split` (topic name, one-line goal, handoff text). If the user gives raw topics instead, normalize them to: name, goal, context needed. `topic-dispatch` does not depend on `status-brief`. If the user happens to have a recent brief at hand, it may be used to notice that a topic already has a live workstream or backlog item, and to attach to it rather than duplicate it.

## Step 1 — Prioritize

Score each topic on four things, in a quick table (high / medium / low, no false precision):

- **Urgency**: a deadline or a cost to waiting.
- **Unblocking power**: does finishing it unlock other topics? (Topics that block others move up.)
- **Effort**: rough size. Cheap wins can go early; very large topics need their own dedicated session.
- **Dependency on the user**: needs a decision or input only the user can give, versus can run on its own.

Order: urgent and unblocking first; among equals, prefer low effort. Limit "now" to a small number (default 3) because the user's problem is too many parallel threads; more open chats defeats the purpose. Say why the cut falls where it does.

## Step 2 — Route each topic

For each topic choose exactly one route:

**A. Dedicated conversation now.** Use for topics ranked in the "now" set. Produce a *starter message* that works with no memory of the original chat: goal, relevant decisions already made (quoted from the source), constraints, files/repos involved, what "done" looks like, and the first concrete step. Rule of thumb: someone who has never seen the original conversation could act on it. Keep decisions the user stated separate from assumptions.

Default delivery is **copy-paste text**, because the user decided not to auto-create conversations for now. Only create a conversation automatically if a tool for it exists in the session and the user has asked for that.

**B. Scheduled task for later.** Use for topics that are not urgent, depend on a future date or event, or exceed the "now" budget. Prepare: a short name, a time (date or recurrence), and a standalone prompt (each firing starts a fresh session with no memory of this chat, so the prompt must carry its own context, like a starter message). Create it with the agent's scheduled-task feature only when the user asked for creation or confirms; when the run is unattended and the user pre-authorized scheduling, create it and report. Never use a session-local timer, it dies with the session. For a one-off reminder in this same conversation, use a delayed message if the agent has one. If the agent has no scheduling feature, hand back the name, time and prompt for the user to set up.

**C. Backlog.** For topics worth keeping but with no date and no urgency: record them so they are not lost and can be picked up later. Each backlog item holds: name, goal, the handoff text (self-contained, as for route A), and the one condition that would revive it. Store each item in **two places**, because they serve different purposes: a Markdown file the user can read, edit and version (`backlog.md`, the readable source of truth), and, if a shared memory service (e.g. Mem0) is connected, a mirror entry (type `backlog`, project = the related project, or `backlog` if none) so that any chat and `status-brief` can find it without file access. Write the `.md` first, then the mirror; if only one is reachable, write that one and say which is missing. If the two disagree later, the `.md` wins. Write only after the user's go-ahead (or when the invocation authorizes it); otherwise present the items in the output for the user to store. The backlog is a list of things to decide on later, not a schedule.

`backlog.md` format (append new items, never rewrite existing ones; to close an item, move it to the "Done / dropped" section with a date):

````markdown
# Backlog

## Open

### <short name> — <project, or "none">
- Added: YYYY-MM-DD (from: <chat or topic-split session, if known>)
- Goal: <one sentence>
- Revive when: <condition or trigger>
- Handoff: <self-contained starter text, as for route A>

## Done / dropped

- YYYY-MM-DD — <short name> — <done | dropped> — <one-line reason>
````

Location: the path given by the user; otherwise `backlog.md` at the root of the repo that holds these skills (hypothesis: `chat-agent-setup`), or, if the user's folders are not reachable, hand the new entries back in the output to paste in.

If a topic is too vague to route, route it to "needs a decision from you" with the precise question, rather than guessing.

## Step 3 — Output

Always end with this structure:

1. **Processing order**: numbered list of all topics.
2. **Now**: topics to start, each with its starter message (code block, ready to paste).
3. **Later**: scheduled tasks (name, when, what it will do) and backlog items (with revival condition, and where they were written: `backlog.md`, the memory service, or both).
4. **Needs your decision**: at most a few precise questions.
5. **Assumptions**: anything inferred.

Do not create anything silently: whatever was created (tasks) is listed with its identifier and schedule.

## Safety and scope

- Creating scheduled tasks or writing backlog entries changes the user's account state: in interactive mode confirm first; in unattended mode create only what the invocation clearly authorized.
- Do not execute the topics. Preparing the starting point is the job.
- Do not rewrite the handoff texts from `topic-split` beyond making them self-contained.

## Open points

- Default size of the "now" set (3).
- Exact location of `backlog.md` (default: root of `chat-agent-setup`; it mixes user data into a skills repo, so a separate notes folder may fit better).
- Whether automatic opening of conversations should become the default once available.
