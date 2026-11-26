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

## Conditional data-integrity sub-check: assigned-to (deprecated, read-only)

The gate additionally binds work items that carry an existing assigned-to edge.
The edge is deprecated in 2.0 and READ-ONLY: the sub-check is a data-integrity
check over edges already present, never an authoring requirement — no new
assigned-to edge is authored. An existing edge is validated:

- Typed target — the assigned-to target must resolve to a member (mbr-) line;
  a target of any other Artifact type is not conformant.
- At-most-one target — assigned-to is single-assignee; a work item carrying
  more than one assigned-to relationship is not conformant.
- Provenance — the assigned-to target must originate from the same repository
  as the referring work item (repository-level provenance); an assigned-to
  target originating outside the work item's repository is not conformant.

The sub-check binds only work items carrying an existing assigned-to edge: work
items without the relationship are unaffected and produce no findings. The
sub-check is evaluated when the gate applies (in-review/done). Removal is
deferred one major — assigned-to (and mbr-) is removed in 3.0.

## Verdict

blocking (transition gated; checked early by eka transition, enforced by eka
sync)
