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

## Verdict

blocking
