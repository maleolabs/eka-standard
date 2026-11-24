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

- Standard corpus version: 1.6 (this specification).
- RSF serialization version: "2" (serializationVersion: "2"); versions "1.1"
  and "1" remain importable and are re-emitted as v2.
- Representation identifiers: eka/structured-json/1 (JSON-native content
  object); eka/structured-text/1 (legacy text content).
- Machine interface schema: eka-cko-v2 (legacy: eka-cko-v1, no longer emitted).
- Object hash: SHA-256(unit.json || content).

## Envelope: provenance (optional)

One optional top-level field records where the unit's knowledge came from:
`provenance`, whose value is one of `human`, `inferred`, or `reconciled`. It is
absent by default.

- An absent `provenance` means **human** — a human asserted the content. The
  default is also the common case, so the two representations carry the same
  claim: undeclared and `human` are not two facts, and no two representations
  of one claim may exist.
- An exporter must therefore omit the default and must never spell it. Writing
  `provenance: human` turns an undeclared claim into a declaration; otherwise
  identical packages then differ in bytes over a distinction the artifact
  format cannot express.
- `inferred` means a classifier proposed the unit from a capture input rather
  than a human writing it; `reconciled` means an automated pass derived it from
  recorded change (recent commits, a staged diff). Both are declarations and
  must survive export, import, and re-export unchanged.
- The value is a closed enum, not an extension point. A value outside it is a
  structural violation of the same class as a malformed `created` (R0, see
  `specification/rules/rule-001.md`).
- This field is not the shr- content field of the same name: that one records a
  builder extraction result (`extracted`). This one is envelope metadata,
  carried by every unit type.
- Changing provenance is an envelope change, so it requires a new revision.

The evidence behind an `inferred` or `reconciled` declaration travels in the
sibling envelope fields documented under *Envelope: provenance capture* below.
The rationale (why an enum and not a score, why the default is represented by
absence) is recorded in the universal capture ADR (ADR-035) and is not
restated here.

## Envelope: provenance capture (optional)

Five optional top-level fields record the capture behind an `inferred` or
`reconciled` unit. All five are absent by default; a unit carrying none of them
is complete, and their absence never blocks import.

- `sourcePromptHash` — lowercase hex SHA-256 of the input the capture was
  derived from: the originating prompt for an `inferred` unit, the git signal
  (changed paths plus commit text) for a `reconciled` one. Only the hash
  travels; the input itself never enters the package.
- `confidence` — the classifier's score for the capture, in the closed interval
  0–1. Absent means undeclared.
- `hasConfidence` — records that a `confidence` was declared. It exists because
  the package unit omits a zero value: `confidence: 0` is a claim ("no
  confidence"), and without the flag it is indistinguishable from an undeclared
  score. A non-zero `confidence` is a declaration with or without the flag, so
  packages written before the flag existed keep their claim. The flag is a
  package-unit field only — a repository artifact declares a confidence by its
  presence.
- `sourceCommitSha` — the commit the reconciler read, when the capture came
  from recorded change rather than a prompt. Absent on an `inferred` unit.
- `captureMeta` — an optional object describing the classification and
  deduplication of the capture. Every field in it is optional too:
  - `classifier` — the versioned, implementation-defined label of the heuristic
    that produced the capture (`keyword-heuristic v1`, `git-heuristic v1`).
    Opaque: the standard fixes the field, not the vocabulary, because the
    heuristic is expected to improve.
  - `dedupeKey` — lowercase hex SHA-256 (64 characters) over the normalized
    captured title. Two captures of the same normalized title share a key;
    deduplication compares keys, never raw titles.
  - `title` — the normalized title text the `dedupeKey` was computed from, so
    the key is explainable and recomputable. Optional because packages produced
    before the field existed carry the key alone, and that is not a defect.
    When both are present they must agree: SHA-256 over `title` equals
    `dedupeKey`. No rule compares them, so a mismatch is a producer defect, not
    an import failure.

Title normalization is fixed — otherwise keys are not comparable across
implementations: lowercase, replace every non-alphanumeric character with a
space, collapse whitespace runs, trim the ends.

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

## Content: applicability declaration (optional)

A knowledge Artifact may declare the paths or modules its constraint binds
through one optional content field, `appliesTo` — the machine-answerable form
of "which constraints must a change to this path satisfy".

- `appliesTo` is an array of repository-relative path patterns. A pattern is a
  literal path or a glob over path segments (`*` within one segment, `?` one
  character, `**` across segments). Patterns are matched against paths relative
  to the repository root, forward-slashed on every platform.
- The field is absent by default. An Artifact that declares no `appliesTo`
  binds no path: it is retrieved by identity, never by path. Absence is not a
  defect — most Artifacts are not path-scoped.
- The declaration is normative for retrieval and advisory for knowledge: it
  does not by itself enforce anything, but a deterministic path-to-constraint
  retrieval returns exactly the Artifacts whose declared scope matches a path —
  the higher-authority constraints that bind it — ordered by authority stratum
  and canonical Identity, one hop, with no similarity search. A path that
  matches no declaration yields an empty set, never an error.
- The constraint families — std-, spec-, adr-, req- (see
  specification/tokens/) — are the typical carriers, because they are the
  higher-authority knowledge a change must satisfy. The field is not restricted
  by type: the constraint families are a retrieval convention, not a closed
  set.
- A malformed pattern (a value that is not a string, or a pattern that cannot
  be interpreted) is a structural violation: the declaration cannot be read, so
  it must be reported, not ignored. A well-formed pattern that matches no path
  in the repository is a warning — a scope may be declared ahead of the code
  that will inhabit it.
- Changing a declaration is a content change, so it requires a new revision
  (the Content change channel, P10).

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
