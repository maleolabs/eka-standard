# Rule R8: Single-writer and Projection Non-writer

## Definition

Every State field has exactly one writer; projections carry no owned State of
other artifacts and never write.

## Requirements

- Every State field has exactly one writer.
- Projections carry no owned State of other artifacts.
- Projections never write.

## Verdict

blocking
