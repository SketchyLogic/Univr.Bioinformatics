---
tags:
  - __CONCEPT
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
# Homology modeling

A template-based method for predicting the 3D structure of a **target protein** using one or more experimentally solved **template structures** with detectable sequence similarity. The most widely used approach when a template with >30% SI is available.

**Five steps**:

1. **Template search**: identify structurally solved homologs using BLAST, PSI-BLAST, or HHpred.
2. **Template selection**: prefer >30% SI, high crystal resolution, relevant organism/function; multiple templates can be combined.
3. **Target-template alignment**: align target to template sequence; errors here propagate directly to the final model.
4. **Model construction**: build 3D coordinates via spatial restraints (MODELLER), rigid-body assembly, loop modeling, and side-chain placement.
5. **Model quality assessment**: check stereochemistry (Ramachandran plot, PROCHECK) and statistical energy ([[DOPE score]], QMEAN).

**Accuracy depends on [[Sequence identity zones|sequence identity zone]]**: in the safe zone (>30% SI), [[Cα RMSD]] ~1–2 Å; in the twilight zone errors increase sharply.

See [[homology-modeling]], [[modeller]], [[sequence-alignment]].
