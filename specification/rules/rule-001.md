# Rule R0: Structural Well-formedness

## Definition

Every artifact must be structurally parseable: a well-formed document whose
frontmatter (or JSON envelope) is syntactically valid and carries the required
identity fields. This is the structural bucket of the Reference Validator:
invalid encoding, malformed frontmatter, unknown top-level fields, non-object
content, and missing required keys are structural violations.

## Requirements

- Every artifact must be structurally parseable: a well-formed document whose
  frontmatter (or JSON envelope) is syntactically valid and carries the
  required identity fields.
- Structural violations include: invalid encoding, malformed frontmatter,
  unknown top-level fields, non-object content, and missing required keys.
- A malformed optional date field (`validUntil`, `lastConfirmed` — see the
  exchange envelope) is a structural violation of the same class as a
  malformed `created`. The field's value is never compared against a clock:
  an artifact past its validity horizon is structurally well-formed.

## Verdict

blocking
