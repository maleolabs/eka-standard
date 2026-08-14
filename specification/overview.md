# Overview

This specification is the versioned snapshot of the EKA Standard 1.0.0. On any
conflict with companion documentation (README, changelog, contribution guide),
this specification wins.

The word "must" denotes a binding requirement on all implementations. The word
"should" denotes a recommendation within the bounds of the standard. The word
"may" denotes an option within the bounds of the standard.

## Identity and Purpose

### Name

Engineering Knowledge Architecture (EKA). Official abbreviation: EKA
(capitalized, no periods, no decoration). Versioned form: "EKA Standard 1.0.0".

### Version

1.0.0.

### Purpose

EKA is the canonical conceptual model for engineering knowledge: the definition
of Artifact, Identity, State, knowledge taxonomies, the layer architecture, and
exchange contracts between systems.

### Scope

This standard establishes concepts, invariants, and contracts. It does not
establish serialization formats, storage layout, directory structure, document
templates, query languages, or specific enforcement mechanisms; those are
implementation decisions that must comply with this standard.

### Reading convention

Capitalized terms are canonical terms defined in this specification (see
concepts.md).

## Description

### What EKA is

EKA is a standard for representing engineering knowledge as first-class
entities — Artifacts — with a stable Identity, an explicit owned State Vector,
structured Content, and Relationships expressed by Identity. It is a conceptual
model, not a product or a tool.

### Problem solved

The standard resolves three persistent problems:

1. Identity instability — knowledge identified by location, file name, or
   process stage breaks when storage or structure changes.
2. Implicit and duplicated state — status scattered across status machines and
   derived views drifts out of sync and cannot be trusted.
3. Knowledge cannot move between systems — without a lossless exchange
   contract, knowledge is trapped in one storage medium.

### Goal

Knowledge survives changes of storage medium and moves between systems without
losing or duplicating Identity, State, Content, or Relationship.

### Scope

The standard covers: fundamental concepts and principles; the layer
architecture and its contracts; the Identity Model; the State Taxonomy;
knowledge, execution, and artifact taxonomies; Engineering Domains and
Knowledge Stratification; the Exchange Contract; conformance rules; naming
convention; and versioning policy.
