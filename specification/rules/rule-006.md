# Rule R5: Referential Integrity

## Definition

Every Relationship reference must resolve to an existing artifact. Draft
artifacts are granted draft tolerance: an unresolved reference on a Draft
artifact is a warning, not a violation.

## Requirements

- Every Relationship reference must resolve to an existing artifact.

## Exceptions

- Draft artifacts are granted draft tolerance: an unresolved reference on a
  Draft artifact is a warning, not a violation.

## Verdict

blocking for non-draft artifacts; warning for Draft artifacts
