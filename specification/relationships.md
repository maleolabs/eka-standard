# Relationship Types

Relationships are recorded on the referring artifact (one-directional) and are
expressed by Identity, never by location, display name, or classification.

## The five canonical Relationship types

- **supersedes** — the referring artifact replaces the target (a new Line
  supersedes an older Line).
- **amends** — the referring artifact amends the target.
- **derives-from** — the referring artifact is derived from the target.
- **depends-on** — the referring artifact depends on the target.
- **validates** — the referring artifact validates the target.

## Two additional Relationship types

- **discusses** — a note (cmt-) points to its subject.
- **repliesTo** — a reply note attaches to exactly ONE parent note
  (single-parent, never nested).

## Deprecated relationship: assigned-to

- **assigned-to** — a work item (sto-, ts-, bug-, td-, ch-, spk-) pointed to
  its assigned member (mbr- line); at most ONE target (single-assignee).
  **Deprecated in 2.0, READ-ONLY**: no new assigned-to edge may be authored;
  existing edges remain recognized and resolvable on read only. Removal is
  deferred one major — assigned-to is removed in 3.0. The member-scoped
  projections (member board, `view --member`, assignee keys) are removed.

## Sharing object rules (shr-)

- A sharing object (shr-) MUST carry `derives-from` to a `rel:` version
  (`rel:<id>:<v>`); versioning is per release.
- A sharing object MUST NOT carry a live `depends-on` to its source.
- `sourceHash` pins the source `objectHash` at release time (see
  tokens/shr.md). Reference: `eka/adr:sharing-object-model:1`.

## Extensibility

New Relationship types are lightweight extensions; packages using non-canonical
types must declare them as Extension Declarations. An importer may reject
undeclared or unknown types.
