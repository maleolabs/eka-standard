# Architectural Principles

## P1 — Separation of Concerns

Knowledge and execution responsibilities are separated into layers with
explicit contracts. Fusing both into a single hierarchy is the source of
conflation.

## P2 — Explicit State

State is always explicit as owned metadata — never implicit in structure.
Structure may be a projection of State, but never an independent fact.

## P3 — Stable Identity

Identity is immutable and independent of location, storage, State, and
classification. References always use Identity, never location.

## P4 — Protocol vs Content Distinction

Protocol is a property of the Operating Layer; Content is a property of the
Knowledge Layer. Every artifact serving both defines the two separately.

## P5 — Layer Independence

Each layer may evolve without overhauling the others: taxonomy changes without
touching protocol; protocol is strengthened without shifting the home of
knowledge.

## P6 — Single Writer

Every State field has exactly one owner. Any other view is a State Projection —
generated or validated, never edited as an independent fact.

## P7 — Forward-Only Transitions

All State Domains move forward without regression. Corrections are made with a
new instance + Relationship, not by mutation.

## P8 — Approved-Content Immutability

Content that has passed the approval gate is not silently mutated. Changes
occur only through the governance channel.

## P9 — Structure as Projection of State

Structural organization and position are derived from State and Identity —
structure never becomes a second fact that can drift from State.

## P10 — Two Change Channels

The Content channel (governance) and the State channel (protocol) are separate.
Mixing them is a violation.

## P11 — Determinism by Protocol

Execution order is defined by protocol: "what next" is always answered.
Enforcement is an implementation capability; the requirement is the standard.

## P12 — Preservation Over Deletion

History is knowledge. Even wrong decisions are preserved. Superseded and
Archived are Records, not garbage.

## P13 — Lossless Exchange

Exchange between systems must not lose or duplicate Identity, State, Content,
or Relationship.

## P14 — Minimum Canonical Core

The standard establishes concepts and contracts; implementations choose
mechanisms. The smaller the core, the longer the life of the standard.

## P15 — Classification is Property, Not Identity

Knowledge Dimension and Engineering Domain are artifact properties; a
classification change never breaks references.

## P16 — Enforcement Capability Varies, Invariants Don't

Enforcement mechanisms differ across implementations (structural constraints,
database constraints, validation); the invariants to be enforced are identical.
