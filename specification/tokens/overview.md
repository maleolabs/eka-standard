# Canonical Tokens

## Token taxonomy rules

The canonical token is part of Identity (the Type qualifier) and is never
methodology-dependent. Methodology terms (PRD, ADR, RFC, Epic, Sprint, Ticket,
Release, Incident, Runbook, and similar) are Representation Aliases mapped onto
a canonical token + Engineering Domain — never frontmatter type values, never
Artifact types in their own right.

The 29 canonical tokens. Each token maps to a Knowledge Dimension and an
Engineering Domain with its stratum. The Engineering Domain and stratum are
derived from the token, never declared by an Artifact.

## Token table

| Token | Knowledge Dimension             | Engineering Domain | Stratum |
| ----- | ------------------------------- | ------------------ | ------- |
| vis-  | intent                          | Discovery          | 1       |
| str-  | intent                          | Discovery          | 1       |
| req-  | requirements                    | Discovery          | 1       |
| fnd-  | research                        | Discovery          | 1       |
| arc-  | architecture                    | Architecture       | 2       |
| adr-  | decisions                       | Architecture       | 2       |
| dec-  | decisions                       | Architecture       | 2       |
| spec- | specifications                  | Architecture       | 2       |
| std-  | standards                       | Architecture       | 2       |
| gls-  | vocabulary                      | Architecture       | 2       |
| scp-  | planning                        | Planning           | 3       |
| epc-  | planning                        | Planning           | 3       |
| plan- | planning                        | Planning           | 3       |
| trc-  | planning                        | Planning           | 3       |
| rvw-  | quality                         | Execution          | 4       |
| ctr-  | operating token (informational) | Execution          | 4       |
| tkt-  | operating token (informational) | Execution          | 4       |
| sto-  | operating token (informational) | Execution          | 4       |
| ts-   | operating token (informational) | Execution          | 4       |
| bug-  | operating token (informational) | Execution          | 4       |
| td-   | operating token (informational) | Execution          | 4       |
| ch-   | operating token (informational) | Execution          | 4       |
| spk-  | operating token (informational) | Execution          | 4       |
| ses-  | operating token (informational) | Execution          | 4       |
| cmt-  | operating token (informational) | Execution          | 4       |
| mbr-  | operating token (informational) | Execution          | 4       |
| run-  | operations                      | Operations         | 5       |
| rel-  | records                         | Operations         | 5       |
| shr-  | records                         | Operations         | 5       |

## Operating tokens (shared explanation)

The operating tokens (ctr-, tkt-, sto-, ts-, bug-, td-, ch-, spk-, ses-, cmt-,
mbr-) share "operating token (informational dimension)" semantics: they are
execution-side Artifacts that carry work through Protocol rather than durable
knowledge. Each operating-token file records only its specific owned State and
identity notes and references this section; the shared explanation is not
repeated per file.

## Note and member tokens

The cmt- (note) artifact type is the 27th token: owned State Vector (Content
State, Existence State, Note State); IsKnowledge false. It carries the
discusses relationship to a subject and the repliesTo relationship to its
single parent note.

The mbr- (member) artifact type is the 28th token: owned State Vector (Content
State, Existence State); IsKnowledge false. It is the typed target of the
assigned-to relationship carried by work items (see relationships.md).

The shr- (sharing object) artifact type is the 29th token: owned State Vector
(Content State, Existence State); IsKnowledge true. It is a snapshot copy
derived from a source CKO at release time carrying level/provenance/
title/description (see tokens/shr.md); never a live projection.

## State Vector attribution

The standard explicitly enumerates State Vectors for work items (sto-, ts-,
bug-, td-, ch-, spk-), plan, Execution Container, ADR, note (cmt-), and Ticket
(empty) in specification/state.md. Existence State applies to all Artifact
types (specification/state.md). The complete type-to-state binding is normative
per Identity rule 5 (specification/identity.md); token files record the domains
the standard attributes.
