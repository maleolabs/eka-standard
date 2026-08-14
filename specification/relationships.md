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

## Extensibility

New Relationship types are lightweight extensions; packages using non-canonical
types must declare them as Extension Declarations. An importer may reject
undeclared or unknown types.
