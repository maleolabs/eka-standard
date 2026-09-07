# Changelog

Semantic changes across versions of the EKA Standard.

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
