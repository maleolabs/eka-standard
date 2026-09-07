# Engineering Domains

## Engineering Domain

The home classification of an Artifact: the stratum-aligned category of
engineering knowledge to which the Artifact belongs. It is a classification
property (P15 — reclassification never touches Identity): derived from the
Artifact's Knowledge Dimension and token family, or declared by an extension;
never Identity, never part of the State Vector.

## Knowledge Stratum

The authority level of an Engineering Domain: a fixed position in the strict
linear order Discovery → Architecture → Planning → Execution → Operations
(stratum 1 highest authority → 5). The stratum is always derived from the
Engineering Domain — never declared by an Artifact, never part of the State
Vector. One Artifact has exactly one Engineering Domain and therefore exactly
one stratum.

## The five canonical Engineering Domains, in stratum order

| Domain       | Stratum | Token families                          | Knowledge Dimensions                                |
| ------------ | ------- | --------------------------------------- | --------------------------------------------------- |
| Discovery    | 1       | vis-, str-, req-, fnd-                  | intent, requirements, research                      |
| Architecture | 2       | arc-, adr-, dec-, spec-, std-, gls-     | architecture, decisions, specifications, standards, vocabulary |
| Planning     | 3       | scp-, epc-, plan-, trc-                 | planning                                            |
| Execution    | 4       | rvw-, ctr-, tkt-, sto-, ts-, bug-, td-, ch-, spk-, ses-, cmt-, mbr- | quality + operating tokens          |
| Operations   | 5       | run-, rel-, shr-                        | operations, records                                 |

## Stratum Authority Invariant

Engineering Domains form a strict linear order by Knowledge Stratum. Knowledge
in a lower stratum must not contradict knowledge in a higher stratum that is in
force (Content State Approved or beyond, or Planning State Immutable); a
discovered contradiction is resolved by changing the lower-stratum knowledge
through the governance channel (new instance + Relationship, forward-only),
never by overriding the higher stratum. A lower-stratum artifact must not
supersede or amend a higher-stratum artifact.

## Stratum vs lifecycle vs Phase

Stratum is an authority property: static per Engineering Domain, fixed at
classification. Lifecycle is the movement of State over time: an Artifact moves
through its State Domains while its stratum does not move. Phase is product
context: a context attribute on planning/scope Artifacts. One Artifact has a
fixed stratum while its lifecycle moves and its Phase context may change.

## Registry governance

Refinement — domain addition, stratum reassignment, or boundary change — is
taxonomy governance (proposal → review → acceptance); a refinement must not
weaken the Stratum Authority Invariant. The Vocabulary dimension (gls-) is
homed in the Architecture domain (very-stable, high-governance knowledge); a
dedicated Vocabulary domain was considered and rejected.
