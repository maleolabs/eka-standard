# Token: shr- — Sharing Object

- **Token ID:** `shr-`
- **Artifact Type:** Sharing Object
- **Knowledge Dimension:** records
- **Engineering Domain:** Operations (stratum 5)
- **Owned State Domains:** Content State, Existence State
- **Identity/relationship notes:** IsKnowledge true. A snapshot copy derived from a source CKO at release time; never a live projection. Reference: `eka/adr:sharing-object-model:1`.

## Required fields

| Field | Type | Required | Notes |
| ----- | ---- | -------- | ----- |
| title | string | yes | Sharing package title, non-empty. |
| description | string | yes | Package content and purpose, non-empty. |
| level | enum `L0\|L1\|L2` | yes | Opt-in depth, see Levels. |
| provenance | enum `extracted` | yes | Builder extraction result (1.3 conformant). |
| sourceHash | string | yes | Object hash as defined in specification/exchange.md (SHA-256(unit.json \|\| content)), hex-encoded opaque string; pins the source `objectHash` at release. |
| sourceRef | relationship `derives-from` | yes | Target `rel:` version (`rel:<id>:<v>`). |

Level and provenance enums are content values, not state values.

## Levels (normative, opt-in)

- **L0** — title, description, sourceRef, sourceHash only (release metadata + source identity, no source content).
- **L1** — L0 + builder-derived safe summary/structure (no sensitive content).
- **L2** — L1 + full content snapshot at sourceHash.

The level is selected explicitly per release. Default share nothing: without an explicit level, nothing is shared.

## Provenance

- `extracted` — builder extraction of a CKO (1.3 conformant).
- `audited` reserved for future extension, not conformant in 1.3.

## Relationship rules

- MUST carry `derives-from` to a `rel:` version (`rel:<id>:<v>`).
- MUST NOT carry a live `depends-on` to the source.
- A new release is a new instance (InstanceVersion pointing to a different instance) with a new `derives-from`.
- R10 note: shr- SHOULD carry transitive upward trace to the source's higher-stratum anchor where known (a derives-from chain reaching a strictly higher stratum); the R10 verdict is warning per rule-011, never a commit blocker; shr- is not in the exempt list (exempt: tkt-, ses-, cmt-, mbr- + drafts).

## Snapshot + pin-hash

shr- content is a frozen copy at release. `sourceHash` pins the source `objectHash`. Consumers fetch without the source repository.

## Opt-in default-deny

Default share nothing. Only fields covered by the explicit level are shared.
