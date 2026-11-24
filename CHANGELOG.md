# Changelog

Semantic changes across versions of the EKA Standard.

## 1.6

- Add the standard check gate to the distributed hooks: `templates/hooks/pre-commit`
  and `templates/hooks/pre-push` now invoke `eka verify --changed` (the
  repository-scope checks the standards declare for the changed set), non-blocking
  by default so the universal-capture contract is preserved
  (sto:verify-changed-gate, M3a stage B).

## 1.5

- Add the applicability declaration: the optional content field `appliesTo`,
  binding a constraint Artifact to the paths or modules it applies to, with a
  deterministic path-to-constraint retrieval and its validation classes
  (specification/exchange.md, specification/concepts.md).

## 1.4

- Add scope-aware container concurrency (specification/concepts.md,
  specification/state.md).
- Add the validity horizon fields `validUntil` and `lastConfirmed`
  (specification/exchange.md, specification/overview.md,
  specification/rules/rule-001.md).
- Add the provenance and capture envelope: `provenance`, `sourcePromptHash`,
  `captureMeta`, `sourceCommitSha` (specification/exchange.md).
- Add the exchange conformance corpus (conformance/exchange/).

## 1.3

- Add the shr- token family (see specification/tokens/shr.md). Reference:
  `eka/adr:sharing-object-model:1`. Canonical token count 28 → 29.
- Add the sharing-object relationship rules: shr- MUST carry derives-from to a
  `rel:<id>:<v>`; MUST NOT carry a live depends-on to its source.
  (specification/relationships.md).

## 1.2

- Add capture hooks (templates/hooks/pre-commit, pre-push) for ADR-035 universal capture (provenance human|inferred|reconciled, non-blocking POSIX hooks distributed via anvil platform_sync).

## 1.1

- Add the mbr- token family (member line; Execution, stratum 4; state vector
  Content State + Existence State; R10 exemption). Canonical token count
  27 → 28.
- Add the assigned-to relationship: a work item (sto-, ts-, bug-, td-, ch-,
  spk-) points to its assigned member (mbr- line), at most one target.
- Extend rule R10 (rule-011.md): the exemption list now covers the tkt-, ses-,
  cmt-, and mbr- tokens, and draft knowledge artifacts.
- Extend rule R13 (rule-014.md): the graph pass adds the conditional
  assigned-to sub-check on work items carrying the relationship (typed target,
  at-most-one target, provenance equality).

## 1.0

- Initial stable EKA Standard.
