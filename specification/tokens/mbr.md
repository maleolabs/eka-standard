# Token: mbr- — Member (deprecated)

- **Token ID:** `mbr-`
- **Artifact Type:** Member
- **Status:** DEPRECATED in 2.0 — READ-ONLY. No new mbr- line may be authored;
  existing lines remain recognized and resolvable on read. Removal is deferred
  one major — mbr- is removed in 3.0.
- **Knowledge Dimension:** operating token (informational)
- **Engineering Domain:** Execution (stratum 4)
- **Owned State Domains:** Content State, Existence State
- **Identity/relationship notes:** IsKnowledge false. The member unit expressed
  human ownership of work: an mbr- line represents a team member, and a work
  item (sto-, ts-, bug-, td-, ch-, spk-) carried at most one assigned-to
  relationship resolving to an mbr- line. Both the token and the assigned-to
  relationship are deprecated (read-only) in 2.0; no new edge is authored.
  Member-scoped projections (member board, `view --member`, assignee keys) are
  removed. Attribution and provenance are retained. The mbr- line is a
  data-model unit (no authentication/authorization semantics). Exempt from R10
  stratification traceability (rule-011.md): a member line is an operating
  record, not durable knowledge.

Operating token — see tokens/overview.md for shared operating-token semantics.
