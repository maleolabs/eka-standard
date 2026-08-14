# Contributing

This repository is the canonical specification/distribution repository of the
EKA Standard. The standard is a documentation-only artifact; there is no code
to run.

## How the standard is structured

The standard has two layers:

- **Detailed specification** — the [`specification/`](specification/) directory
  is the source of truth for detail semantics: `rules/` (one file per
  conformance rule), `domains/`, `tokens/`, and the concept documents
  (`overview.md`, `principles.md`, `concepts.md`, `identity.md`, `state.md`,
  `dimensions.md`, `relationships.md`, `naming.md`, `exchange.md`,
  `versioning.md`). This is the deep reference for maintainers, developers,
  and agents.
- **Canonical reference** — the [`EKA`](EKA) file (no extension, plain text) is
  a compact summary and index that points into `specification/`. It is a
  distribution artifact for consumer projects, not a definition.

On any conflict, **`specification/` wins over `EKA`**, `README.md`, and this
guide. A change to the detailed specification must trigger a review of the
`EKA` summary so the two never drift apart.

## Immutability and versioning policy

- EKA Standard **1.0 is immutable** — it is never edited in place.
- Normative changes require a version bump per semantic versioning:
  - **1.1** — backward-compatible normative changes (additive: new sections,
    clarifications, subordinate terms, additive rule definitions).
  - **2.0** — breaking changes (amends invariants, changes verdict semantics,
    redefines a canonical term, changes a naming pattern).
- Foundations that never change: Identity, the global invariants, the
  two-change-channel separation, and the layer composition (KB + OS + EX).

## Proposing a change to the standard

1. **Open an issue** describing the proposed change and why it is needed.
2. **Classify the change** — normative (affects `specification/` and possibly
   the `EKA` summary) or informative (docs only). Normative changes must state
   the target version bump.
3. **Discuss** with the EKA maintainers. A proposal must not weaken invariants
   or the Stratum Authority Invariant.
4. **Review** — the maintainers evaluate the change against the conformance
   rules (R0–R13) and the versioning policy.
5. **Publish** — accepted normative changes land in the detailed
   `specification/` files at the new version, the `EKA` summary is updated to
   match, and a `CHANGELOG.md` entry is added. Informative changes are applied
   to the Markdown docs directly.

## Where design decisions live

Architecture decisions, design records, and ADRs are Engineering Knowledge and
live in the EKA knowledge system — not in this repository. This repository
holds only the versioned standard text and its documentation.

## Language and style

- Normative text is written in English; English is the canonical language.
- Terminology is fixed by the standard (the `specification/` directory). Do not
  introduce new terms without a terminology review.
- "must" = binding requirement, "should" = recommendation, "may" = option.
