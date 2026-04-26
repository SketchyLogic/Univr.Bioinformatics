---
tags:
  - __EXECUTABLE
  - Module1
CreatedAt: 2026-04-25
LastUpdateAt: 2026-04-25
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedById: claude-sonnet-4-6
---
# Compare PWM, WAM, and MDD for splice site modeling

| Model | What it captures | Assumption | Limitation |
|-------|-----------------|------------|------------|
| [[Position Weight Matrix (PWM)\|PWM]] | Nucleotide frequency at each position independently | Positions are **independent** | Cannot model position correlations |
| [[Weight Array Model (WAM)\|WAM]] | Pairwise dependencies: P(sⱼ \| sⱼ₋₁) | Adjacent positions may depend on each other | Only captures **first-order** (adjacent) dependencies |
| [[Maximal Dependence Decomposition (MDD)\|MDD]] | Non-adjacent, context-specific dependencies via a decision tree of WAMs | Different sub-contexts need different models | Requires **large training set**; complexity increases |

**Progression**: PWM → WAM → MDD represents increasing model expressiveness at the cost of larger data requirements and more complex training.

**When to use each**:
- **PWM**: sparse training data or when correlations are weak.
- **WAM**: known adjacent correlations (e.g., GT at donor sites is not two independent positions).
- **MDD**: strong non-adjacent dependencies exist and enough training data is available; [[genscan|GENSCAN]] uses MDD for its donor splice site model.

**Exam tip**: if asked "what assumption does a PWM violate?" → positional independence. If asked "what does a WAM add?" → first-order Markov dependencies between adjacent positions.

See [[signal-sensors]], [[genscan]].
