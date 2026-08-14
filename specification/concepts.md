# Core Concepts and Layer Model

## Layer Model

The architecture has exactly three layers, bound together by Identity.

### Knowledge Layer (KB)

The knowledge store: Content, classification, preservation, references. Owns:
Content; classification (Knowledge Dimensions); Relationship; history/Records;
Identity administration (Identity Registry). Does not own: process State,
execution Protocol.

### Operating Layer (OS)

The state machine and execution Protocol. Owns: State Domains (Execution,
Planning, Container, Existence), ordering, concurrency, locking, Gates,
Command. Does not own: Content (never edits Content).

### Exchange Layer (EX)

The transformational boundary: serialization, validation, import/export,
mediation of external systems. Owns: exchange contracts, round-trip rules,
conformance validation. Does not own: Content and State (never becomes an
owner).

### Layer independence

KB may change its taxonomy without changing OS Protocol (P5). OS may add
protocol variants without changing KB classification. EX may add serialization
formats without changing KB/OS. All three are bound by Identity, the global
invariants, and the inter-layer contracts.

### Global invariants

1. Identity immutable — Identity is not changed by State, location,
   classification, or Content revision (P3).
2. Single owner per State field — one writer; all other views are State
   Projections (P6).
3. Structure as projection of State — structural position is derived from
   State, never an independent fact (P9).
4. State changes only via Protocol — no State change path exists other than
   Protocol transitions (P11).
5. Two separate change channels — the Content channel and the State channel
   never mix (P10).
6. Approved Content immutable — preservation (P8, P12).
7. Round-trip lossless — exchange loses and duplicates nothing (P13).

## Core Concepts

### Artifact

An engineering knowledge entity that has Identity, Content, a State Vector (the
State Domains it owns), and Relationship. The basic unit of the model.

### Content

The semantic payload of an Artifact: intent, decisions, design, constraints,
procedures, notes. Belongs to the Knowledge Layer.

### Well-formed Content

Content that conforms to the structure established for its Artifact type, so
that it can be parsed and executed deterministically.

### Identity

The property of an Artifact that permanently distinguishes it from all other
Artifacts. See identity.md.

### Artifact Line

The enduring Identity entity: one (Namespace, Type, ID).

### Artifact Instance

One version of a Line's existence: Line + InstanceVersion.

### State

A fact about the position of an Artifact within a given process.

### State Vector

The tuple of State Domains owned by an Artifact. Projected State (State
Projection) is not part of the State Vector.

### State Domain

An independent State dimension with its own semantics, owner, and transition
rules (see state.md). Domains are orthogonal.

### State Projection

A State view derived from its owner (example: aggregate of work item State
producing Execution Container status). A projection has no State of its own; a
projection never becomes a writer.

### Projection Semantics

The computation rules of a State Projection: from which owner, how aggregation
works, what is displayed.

### Projection Refresh

The mechanism and timing of State Projection validation against the owner
(on-read and/or event).

### Knowledge Dimension

An axis of knowledge classification (see dimensions.md). An Artifact property,
not Identity.

### Protocol

Deterministic rules owned by the Operating Layer: ordering, State transitions,
locking, gates, execution commands.

### Namespace

An Identity space that separates management domains (products, organizations,
systems).

### Relationship

An explicit relation between Artifacts referenced by Identity. See
relationships.md.

### Gate

A condition that must be satisfied before a transition or execution may occur
(approval gate, readiness gate, review gate).

### Command

A deterministic execution instruction consumed by an executor (human or agent).
Command Content is Content (owned by the Knowledge Layer); its execution is
governed by Protocol (Operating Layer).

### Execution Container

An execution Artifact that wraps work items and carries a concurrency
convention (exactly-one-active). Its State Domain: Container State.

### Phase

Product/scope context over time (Discovery, MVP, Milestone, Release). Phase is
a context attribute on planning/scope Artifacts: not a category, not a State
Domain. Phase change is a context update authorized by a readiness Gate.

### Record

An Artifact preserved as history (Superseded, Archived, Retired, release
record) with immutable Content.

### Distillation

Transformation of ephemeral knowledge (working context, review findings) into
durable knowledge (decisions, ADRs, Records).

### Change Log

The chronological record of State transitions on an Artifact: domain, old
value, new value, time, authority. Mandatory for all State Domains.

### Identity Registry

A Knowledge Layer function that guarantees Identity uniqueness, Identity
resolution to Artifacts, and referential integrity.

### Trigger

A relationship between domains/operations in which an event triggers
validation or a transition in another domain.

### Knowledge OS

A future knowledge execution platform that consumes and produces EKA Artifacts
through the Exchange Layer. Not part of the standard; a consumer of the
standard.
