# Changelog

Semantic changes across versions of the EKA Standard.

## 1.3

- Add the shr- token family (sharing object; records; Operations, stratum 5;
  state vector Content State + Existence State; IsKnowledge true). Required
  fields: title/description (non-empty), level L0|L1|L2, provenance
  extracted|audited (MVP: extracted only), sourceHash (pin source objectHash),
  sourceRef (derives-from rel:versi). Snapshot copy + pin-hash at release;
  no live depends-on. Opt-in levels L0-L2, default-deny (default share
  nothing). Acuan: ADR sharing-object-model. Canonical token count 28 → 29.
- Add the sharing-object relationship rules: shr- MUST carry derives-from to a
  rel: version; MUST NOT carry a live depends-on to its source.
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
