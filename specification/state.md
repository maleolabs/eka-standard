# State Taxonomy

## State Domains

An Artifact carries a State Vector — the tuple of State Domains it owns per its
type. Domains that do not apply are marked not-applicable. Every domain has
exactly one initial state and exactly one terminal state; all transitions are
forward-only (P7); corrections are made with a new instance + Relationship,
never regression. Domain values cover only owned State; derived conditions (for
example "Completed" in a working context) are transition-triggering conditions,
not domain values.

## Owned State Domains

### Content State

Values: Draft → Review → Approved; post-approval terminal: Amended |
Superseded. Responsibility: content maturity as knowledge; the governance
channel. Owner: Knowledge Layer (gate: owner/approver). Forward-only; approval
gate; changes after Approved only via amendment/supersession (P8). Variants:
standard (terminal Amended), decision record (approval stage named Accepted;
supersession optional), ADR (approval stage named Accepted; supersession must
point to a successor). Variants may rename stages and eliminate optional
stages, but must preserve the semantic position: pre-approval → approval gate →
post-approval terminal.

### Execution State

Values: Planned → Todo → In Progress → In Review → Done, plus Canceled.
Responsibility: work item progress through Protocol. Owner: Operating Layer
(single-writer: work item artifact). Transition rule (D1): forward adjacent
Planned → Todo → In Progress → In Review → Done; one-step pull-back In Review →
In Progress and In Progress → Todo; → Canceled from any state; re-activation
Canceled → Todo. Done is terminal.

### Planning State

Values: Draft → Approved → Immutable. Responsibility: plan commitment
(tentative → committed → locked). Owner: Operating Layer. Forward-only;
Approved = ready for execution; Immutable is reached atomically with the
Execution Container creation event (lock-atomic-with-generation); post-lock
changes = new instance (InstanceVersion).

### Container State

Values: Active → Completed. Responsibility: Execution Container open/closed;
concurrency. Owner: Operating Layer. Completed is a derived transition,
triggered by the Execution State aggregate (all work items Done);
scope-aware concurrency: one Active container per source_repo (the
repository owning the container line), plus a no-dependency gate — the
transitive depends-on/derives-from plan closure of an Activating
container must be disjoint from the closure of every other Active
container; a shared node refuses activation naming the shared plan/edge
(parallel execution across repositories, dec:parallel-container-execution).

### Existence State

Values: Active → Archived → Retired. Responsibility: artifact presence in
active process vs preservation. Owner: Operating Layer (transitions); Knowledge
Layer (preservation principle, P12). Forward-only; Archived = reference-only
(no other State transitions, no Content mutation, still available in
retrieval); Retired = terminal preservation (not surfaced in normal retrieval,
Content immutable, Identity unchanged). Applies to all Artifact types.

### Note State

Values: open → resolved → dismissed, forward-only. Owned only by the cmt-
(note) artifact type. A note is resolved explicitly (never by silent file
edits); the Change Log records the note-state transition with the authority
identity.

## State Vector examples

Work item = (Execution State, Existence State); plan = (Content State, Planning
State, Existence State); Execution Container = (Container State, Existence
State); ADR = (Content State, Existence State); note (cmt-) = (Content State,
Existence State, Note State).

## Empty State Vector

An Artifact whose entire State is projected has an empty State Vector (example:
Ticket = empty; its State is a State Projection over the referenced work item).
Projected State is regenerated at the target via Projection Refresh — a
projection is never exchanged as a source of truth and never becomes a writer
(P6, P9).

## Domain interactions

Execution Container creation triggers the plan's transition to Immutable
(atomic, lock-atomic-with-generation). The work item State aggregate (all Done)
triggers container Completed. An Immutable plan gates Content changes on that
instance. Content readiness is a precondition of plan Approval. A finished
container may be archived. A release readiness Gate evaluates the aggregate
(Execution + Planning + Container + review gate + approval gate) to authorize a
Phase change (a context update, not a State transition).

## Independence

State Domains remain independent (not unified): different semantics require
different machines; different owners (KB vs OS); different rates of change.
Interactions are managed explicitly via Triggers and Gates, not by merging
domains.
