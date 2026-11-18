# Exchange and Serialization Essentials

Normative essentials of the Exchange Contract. The contract is conceptual; any
concrete serialization is an implementation that must satisfy it.

## Exchange unit

The smallest exchange unit is the Artifact Instance: one instance carrying
complete Identity, Content, State Vector (all owned domains), Change Log,
Relationships, and classification. Selection is permitted only at unit
granularity; partial state exchange (a subset of owned domains) is forbidden.

## Lossless round-trip

Exchange must not lose or duplicate Identity, State, Content, Relationship, or
classification (P13). Import must be idempotent: re-importing an identical
package is a no-op. Identity conflict policy: reject or explicit re-namespace,
never silent merge. Validation before commit; revalidation after import.

## Serialization essentials

- Standard corpus version: 1.3 (this specification).
- RSF serialization version: "2" (serializationVersion: "2"); versions "1.1"
  and "1" remain importable and are re-emitted as v2.
- Representation identifiers: eka/structured-json/1 (JSON-native content
  object); eka/structured-text/1 (legacy text content).
- Machine interface schema: eka-cko-v2 (legacy: eka-cko-v1, no longer emitted).
- Object hash: SHA-256(unit.json || content).

## Envelope: validity horizon (optional)
Two optional top-level fields record when knowledge stops being trustworthy:
`validUntil` (the declared validity horizon) and `lastConfirmed` (when a human
last asserted the content still holds). Both are absolute dates in
`YYYY-MM-DD` form and both are absent by default.

- An absent `validUntil` means **undeclared** — neither fresh nor stale. There
  is no default horizon: a default would be a guess presented as knowledge.
- `lastConfirmed` is not `updated`: the latter is the file modification time;
  the former is an author-written assertion, never written automatically.
- The fields are advisory. Their **shape** is structural — a malformed date is
  a structural violation of the same class as a malformed `created` — but no
  rule compares either value against a clock. Expiry never blocks, and a far
  horizon is not more conformant than a near one.
- Changing a horizon is an envelope change, so it requires a new revision.

The rationale (why a date and not a duration, why advisory, why no defaults)
is recorded in the freshness ADR and is not restated here.

## Package composition

An Exchange Package contains exactly: a Contract Header (exchange format
version + specification version + exporter identity + export scope + integrity
data); a Manifest (ordered list of all units); zero or more Exchange Units;
Declarations (Closure, External Reference, Extension); and integrity data.
Deterministic ordering by canonical Identity key.

## Sharing object self-containment

A shr- unit is self-contained at release (snapshot + sourceHash); consumers
resolve via sourceHash without the source repository.

## Determinism

Identical repository state must produce identical packages (up to permissible
differences: physical layout, storage addressing, projection refresh
timestamps, package metadata). Package digest semantics: SHA-256 over unit.json
and canonical content bytes.
