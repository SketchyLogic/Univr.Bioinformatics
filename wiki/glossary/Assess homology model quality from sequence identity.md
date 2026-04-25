---
tags:
  - __EXECUTABLE
  - Module2
depth: 2
---
# Assess homology model quality from sequence identity

Use the [[Sequence identity zones|sequence identity zone]] as the first-pass predictor of model reliability, then apply quantitative checks:

**Step 1 — Check sequence identity zone**:

| SI range | Zone | Expected quality | Recommendation |
|----------|------|-----------------|----------------|
| > 50% | Safe | Cα RMSD ~1 Å; side chains may err at interfaces | Good for drug docking |
| 30–50% | Safe | Cα RMSD ~1.5–2 Å; loops may diverge | Acceptable; check loops |
| 10–30% | Twilight | Large errors in misaligned regions | Use with caution; validate |
| < 10% | Midnight | Not reliable | Do not use homology modeling |

**Step 2 — Compute/inspect the [[DOPE score]]**:
- Generate ≥10 models with MODELLER, pick the one with the lowest DOPE score.
- Examine the residue-by-residue DOPE profile to locate problematic regions (peaks = poorly modeled loops).

**Step 3 — Stereochemistry checks**:
- **Ramachandran plot** (PROCHECK): >90% of residues should fall in favored regions.
- **WHATCHECK / QMEAN**: check bond lengths, angles, side-chain rotamers.

**Step 4 — Validate critical regions separately**:
- Check [[Cα RMSD]] in the active site and binding pocket, not just globally.
- If RMSD in the active site > 1.5 Å, docking or function prediction results may be unreliable.

See [[homology-modeling]], [[modeller]], [[DOPE score]], [[Cα RMSD]].
