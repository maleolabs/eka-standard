# EKA Standard

**Engineering Knowledge Architecture (EKA)** is the canonical conceptual model
for engineering knowledge: the definition of Artifact, Identity, State,
knowledge taxonomies, the layer architecture, and exchange contracts between
systems.

This repository is the canonical specification/distribution repository of the
EKA Standard, version **1.0**.

## Two-layer structure

The standard is organized into two layers:

- **`specification/`** — the detailed normative specification. The source of
  truth. Per-concept Markdown files for maintainers, developers, and agents who
  need the full definitions, invariants, and rules.
- **`EKA`** — a compact canonical consumer reference (extension-less, plain
  text). A distribution artifact: a short summary of version, purpose,
  principles, rules, domains, and tokens, with pointers into
  `specification/`.

> **`EKA` is a summary, not the source.** The `EKA` file summarizes and indexes
> the standard; it does not reproduce full definitions. The `specification/`
> directory is authoritative for detail semantics. On any conflict,
> `specification/` wins over `EKA`, `README.md`, the changelog, and the
> contribution guide.

## What the standard defines

EKA Standard 1.0 is a documentation-only specification. It defines:

- the architectural principles (P1–P16);
- the three-layer architecture (Knowledge, Operating, Exchange);
- the Identity Model and the State Taxonomy;
- the five Engineering Domains and Knowledge Stratification;
- the 12 Knowledge Dimensions and 27 canonical tokens;
- the Exchange Contract essentials;
- the Conformance Rules R0–R13.

## Using the standard

1. Reference the [`EKA`](EKA) file for a compact overview, or copy the whole
   [`specification/`](specification/) directory for the full normative text.
2. Treat the standard as versioned and immutable (see `CHANGELOG.md`).
3. Implementations are separate repositories and are not in this repo.

## Relationship to implementations

This repository defines the standard and contains no implementation code.
Implementation artifacts live in separate repositories:

- **`eka-core`** — the Reference Implementation (Knowledge Layer, Operating
  Layer, Exchange Layer).
- **`eka-cli`** — the Reference Validator (the `eka` command-line tool).
- **`eka-mcp`** — the MCP server.
- **`eka-sdk-<language>`** — language SDKs.

An implementation is one serialization of this architecture — not the
architecture itself. Every implementation must satisfy the standard's
invariants, provide Identity resolution, and support lossless exchange through
the Exchange Layer contract.

## Versioning

The following version axes are distinct and must not be conflated:

| Axis | Value | Notes |
|---|---|---|
| Standard corpus version | **1.0** | the versioned snapshot in `specification/` |
| RSF serialization format | `serializationVersion: "2"` | serialization format |
| Representation identifiers | `eka/structured-json/1`, `eka/structured-text/1` | content representation |
| Machine interface schema | `eka-cko-v2` (legacy: `eka-cko-v1`) | machine schema |

See `CHANGELOG.md` for the semantic changes across versions.

## Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md). Changes to the standard follow the
immutability/versioning policy: version 1.0 is immutable; normative changes
require a version bump (1.1 backward-compatible, 2.0 breaking). Design
records and ADRs live in the EKA knowledge system, not in this repository.

## License

Apache License 2.0 — see [`LICENSE`](LICENSE).
