# Rule R2: Identity Canonical

## Definition

Identity must be serialized losslessly, unambiguously, and machine-parseably;
it must never be encoded in location, file name, path, process stage, or
representation convention. Identity lives in the file body, never in filenames
or directories.

## Requirements

- Identity must be serialized losslessly, unambiguously, and
  machine-parseably.
- Identity must never be encoded in location, file name, path, process stage,
  or representation convention.
- Identity lives in the file body, never in filenames or directories.

## Verdict

blocking
