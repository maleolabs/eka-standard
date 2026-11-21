# Versioning and Immutability

## Versioned snapshot

This specification is the versioned snapshot of the EKA Standard 1.4 — an
immutable normative specification. Version 1.4 is frozen; it is never edited
in place. Versions 1.3 and earlier remain frozen.

## Versioning rules (semantic)

- **1.0** — initial stable EKA Standard. Immutable.
- **1.1** — backward-compatible normative changes (additive: new sections,
  clarifications, subordinate terms, additive rule definitions). All existing
  conformant artifacts remain conformant.
- **1.2** — backward-compatible additive: capture hooks (templates/hooks) for ADR-035 universal provenance distribution.
- **1.3** — backward-compatible additive: shr- token family (see tokens/shr.md).
  Canonical token count 28 → 29. All existing conformant artifacts remain
  conformant.
- **1.4** — backward-compatible additive: scope-aware container concurrency;
  the validity horizon fields `validUntil`/`lastConfirmed`; the provenance and
  capture envelope (`provenance`, `sourcePromptHash`, `captureMeta`,
  `sourceCommitSha`). All existing conformant artifacts remain conformant.
- **2.0** — breaking changes (amends invariants, changes verdict semantics,
  redefines a canonical term, changes a naming pattern).

Freezing binds at the declaration, not at the git tag: once this document names
a version as the frozen snapshot, a further normative change — including
documenting an already-implemented optional field — belongs to the next version.
The tag is a release convenience, not the freezing event.

## Distinct version axes (must not be conflated)

| Axis                        | Value                           | Notes                  |
| --------------------------- | ------------------------------- | ---------------------- |
| Standard corpus version     | 1.4                           | this specification     |
| RSF serialization version   | "2"                             | serialization format   |
| Representation identifiers  | eka/structured-json/1, eka/structured-text/1 | content representation |
| Machine interface schema    | eka-cko-v2 (legacy eka-cko-v1)  | machine schema         |

## Immutability of foundations

Evolution never changes: Identity (P3), the global invariants, the
two-change-channel separation (P10), and the layer composition (KB + OS + EX).
What may evolve: taxonomies (dimensions, types, domains, protocol) through
extension governance. The Stratum Authority Invariant can only be strengthened,
never weakened.
