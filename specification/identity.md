# Identity Model

## Identity composition

Identity instance = (Namespace, Type, ID, InstanceVersion).
Identity line     = (Namespace, Type, ID).

| Property                              | Part of Identity?            |
| ------------------------------------- | ---------------------------- |
| Namespace                             | Yes                          |
| Type (Artifact Type)                  | Yes                          |
| ID                                    | Yes                          |
| InstanceVersion                       | Yes (instance discriminator) |
| Knowledge Dimension (classification)  | No                           |
| Engineering Domain (classification)   | No                           |
| Location / organization               | No                           |
| Storage backend                       | No                           |
| State (all domains)                   | No                           |
| Revision (Content edit history)       | No                           |

Namespace separates Identity spaces (products, organizations, systems). Two
Artifacts with the same ID in different Namespaces are two Artifacts. Type
determines the applicable State Domains and the binding Protocol; Type is an
Identity qualifier, not a classification. ID is unique within
(Namespace, Type). InstanceVersion distinguishes instances within one Line.

## Identity rules

1. Identity is established once at creation and never changed.
2. ID is unique within (Namespace, Type); InstanceVersion is unique within a
   Line.
3. References are always by Identity — never by location, display name, or
   classification.
4. Two Artifacts are the same if and only if their Identity is the same;
   Relationship never changes Identity.
5. Artifact Type determines the applicable State Vector (see state.md); the
   type-to-state binding is part of the standard, not an implementation choice.
6. Identity must be serializable losslessly, unambiguously, and
   machine-parseably in all implementations. The serialization mechanism is an
   implementation decision.
7. Supersession, amendment, and derivation are expressed as Relationships
   between Identities, not as Identity changes.

## Canonical serialization contract

Identity must be serialized:

- losslessly — the tuple round-trips without information loss;
- unambiguously — one representation corresponds to exactly one Identity; no
  two representations of one Identity;
- machine-parseably — parseable without human interpretation;
- independently — never dependent on location, file name, path, process stage,
  or representation conventions. Identity lives in the artifact body, never
  encoded in filenames or directories.

## Canonical ordering key

Identity tuples are compared component-by-component in the order (Namespace,
Type, ID, InstanceVersion), with a total, stable comparison over the canonical
serialization of each component.

## Version semantics

Two meanings of version, two answers:

- InstanceVersion — the version pointing to a different instance — part of the
  instance Identity. A new instance is created deliberately (example: plan v2
  after v1 is locked). Instance change = instance Identity change; the Line
  remains.
- Revision — tracking the Content evolution of the same instance — not part of
  Identity. Revision changes on every edit and must not break references.

Rule: Line Identity never changes; instance Identity changes only when a new
instance is deliberately created; Revision never touches Identity. Supersession
is a Relationship between two Lines, not an Identity replacement.
