---
tags:
  - __DEFINITION
  - Module2
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
# HADDOCK scoring function

The empirical scoring function used by [[molecular-docking|HADDOCK]] to rank docking poses after the three-step protocol.

**Final score formula**:

```
HADDOCK score = 1.0 × Elec + 1.0 × vdW + 1.0 × Dsolv + 1.0 × AIR
```

| Term | Physical meaning |
|------|-----------------|
| **Elec** | Coulomb electrostatic energy |
| **vdW** | Van der Waals energy (Lennard-Jones) |
| **Dsolv** | Desolvation energy (ACE continuum model) |
| **AIR** | Sum of [[Ambiguous Interaction Restraint (AIR)|AIR]] restraint violation energies |

**Workflow after scoring**:
1. All refined poses are clustered by interface RMSD (typically cutoff 7.5 Å).
2. Clusters are ranked by average HADDOCK score.
3. The top cluster(s) represent the predicted binding mode(s).

The **lower** the HADDOCK score, the better the pose.

See [[molecular-docking]].
