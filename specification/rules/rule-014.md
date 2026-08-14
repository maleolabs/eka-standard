# Rule R13: Graph Pass (Note Resolution Gates)

## Definition

The second conformance pass resolves discusses edges across the analyzed set. A
work item at in-review requires at least one child note with role
implementation and note-state resolved; a work item at done requires every
child note resolved. The gate reads the note's current note-state (latest
instance). Replies (role reply, repliesTo edges) are not evidence: they never
satisfy a gate on their own.

## Requirements

- A work item at in-review requires at least one child note with role
  implementation and note-state resolved.
- A work item at done requires every child note resolved.
- The gate reads the note's current note-state (latest instance).
- Replies (role reply, repliesTo edges) are not evidence: they never satisfy a
  gate on their own.

## Verdict

blocking (transition gated; checked early by eka transition, enforced by eka
sync)
