---
name: topic-split
description: "Detects when a conversation has drifted into several independent topics and, if so, splits it: lists the topics and writes a self-contained handoff text for each one. Use when a chat mixes unrelated subjects, when the user says 'on part dans tous les sens', 'sépare ça en sujets', 'split this conversation', 'je mélange plusieurs choses', or when a new subject appears that has nothing to do with the current goal. It only separates topics and writes handoffs; deciding what happens to each topic (new chat, scheduled task, backlog) is the job of topic-dispatch."
---

# topic-split

## Purpose

Long chats accumulate subjects that have nothing to do with each other. Each extra subject makes the conversation harder to resume and hides where things stand. This skill separates them, so each topic can be handled on its own.

It stops at the separation. It does not prioritize, open conversations, schedule tasks or store a backlog: that is `topic-dispatch`. It does not execute the topics either.

## When to use

- The user asks to split or untangle a conversation.
- A new subject appears in a chat, independent from the current goal (different project, different deliverable, different people involved).
- The conversation is long and the user wants to know what is in it before continuing.

## Step 1 — Decide: split or not

Two subjects are **independent** if one can be finished, postponed or dropped without changing the other. A question that merely supports the main goal, or a detour that will be resolved in the same chat, is not a separate topic.

When in doubt, **do not split**. Say so in one sentence with the signals that justify it, and stop. Over-splitting creates more chats to track, which is the problem this skill exists to reduce.

## Step 2 — List the topics

For each independent topic:

- **Name**: short, specific (a slug works).
- **Goal**: what it is trying to achieve, in one sentence.
- **State**: where the discussion stopped (decided / open / blocked), dated if the conversation gives dates.
- **Origin**: where in the conversation it came from, so the user can check.

Cover the whole conversation, including the main topic. Do not invent topics: each one must be traceable to something said in the chat. If a subject is mentioned in one line and never developed, list it as a minor item instead of a full topic.

## Step 3 — Write one handoff text per topic

The handoff lets a fresh conversation (or the same user a week later) continue the topic **without access to the original chat**. Include:

- the goal;
- decisions already made, as stated by the user, kept separate from assumptions;
- constraints, files, repos, links or names involved;
- what is still open, and what "done" looks like if the conversation said;
- the first concrete step.

Write only the final state, not the history of how the discussion got there. Keep each handoff short enough to paste in one go. The handoff stays **copy-paste text**: this skill does not create conversations.

## Step 4 — Present and validate

Show the decision (split or not), the topic list and the handoffs. Splitting is the user's call, so confirm that the list is right (topics merged or dropped) before treating it as final. In an unattended run, deliver the result as is and flag that it was not validated.

## Output

```
Decision: <split | no split> — <one-sentence justification>

Topics
1. <name> — <goal> — <state>
2. ...

Handoffs
### <name>
<self-contained text>
```

End with one line pointing to `topic-dispatch` for deciding what to do with each topic. Do not start that step uninvited.

## Interface with the rest

`topic-dispatch` consumes exactly: name, goal, handoff text (state and origin are informative). Keep those three fields stable.

## Out of scope

- Prioritizing, opening chats, scheduling, backlog (`topic-dispatch`).
- Progress overview across chats (`status-brief`).
- Working on the topics themselves.

## Open points

- The original topic-split text was lost; this is a rewrite from the project notes (splits independent topics, one handoff per topic, copy-paste, no automatic conversation creation). Compare it with any older copy before adopting it.
