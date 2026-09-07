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

## Three additional Relationship types

- **discusses** — a note (cmt-) points to its subject.
- **repliesTo** — a reply note attaches to exactly ONE parent note
  (single-parent, never nested).
- **assigned-to** — a work item (sto-, ts-, bug-, td-, ch-, spk-) points
  to its assigned member (mbr- line); at most ONE target
  (single-assignee).

## Sharing object rules (shr-)

- A sharing object (shr-) MUST carry `derives-from` to a `rel:` version
  (`rel:<id>:<versi>`); versioning is per release.
- A sharing object MUST NOT carry a live `depends-on` to its source.
- `sourceHash` pins the source `objectHash` at release time (see
  tokens/shr.md). Acuan: ADR sharing-object-model.

## Extensibility

New Relationship types are lightweight extensions; packages using non-canonical
types must declare them as Extension Declarations. An importer may reject
undeclared or unknown types.
