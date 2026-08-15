# Naming Convention

Lower camelCase, deterministic: the first word is lowercase, subsequent words
are capitalized, no separators. Single-word keys stay as-is (type, id, domain,
phase, scope, count). Abbreviations keep their casing per word (objectHash,
packageDigest, unitDigest, canonicalIdentityForm, instanceVersion).

- **State Domain names:** contentState, executionState, planningState,
  containerState, existenceState; noteState (only note units carry it).
- **Relationship type names:** dependsOn, derivesFrom, validates, supersedes,
  amends; discusses, repliesTo, assignedTo.
- **Content section keys:** derived from the section registry names
  deterministically — lowercase the first word, capitalize subsequent words,
  drop non-alphanumeric separators. Examples: "Alternatives Considered" →
  alternativesConsidered; "Acceptance Criteria" → acceptanceCriteria; "Out of
  Scope" → outOfScope; "Work Items" → workItems; "Projected Status" →
  projectedStatus; "Change Log" → changeLog; "Investigation Summary" →
  investigationSummary.

State VALUES are unchanged by the naming convention (lowercase, e.g.
"accepted", "in-progress", "in-review"); only keys are camelCase. What an
author writes is what a consumer reads (WYSIWYG).
