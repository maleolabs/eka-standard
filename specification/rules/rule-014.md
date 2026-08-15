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

## Conditional sub-check: assigned-to

The gate additionally binds work items that carry an assigned-to relationship:

- Typed target — the assigned-to target must resolve to a member (mbr-) line;
  a target of any other Artifact type is not conformant.
- At-most-one target — assigned-to is single-assignee; a work item carrying
  more than one assigned-to relationship is not conformant.
- Provenance — the assigned-to target must originate from the same repository
  as the referring work item (repository-level provenance); an assigned-to
  target originating outside the work item's repository is not conformant.

The sub-check binds only work items carrying assigned-to: work items without
the relationship are unaffected and produce no findings. The sub-check is
evaluated when the gate applies (in-review/done).

## Verdict

blocking (transition gated; checked early by eka transition, enforced by eka
sync)
