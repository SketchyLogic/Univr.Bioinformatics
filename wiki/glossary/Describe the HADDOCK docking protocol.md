---
tags:
  - __EXECUTABLE
  - Module2
---
# Describe the HADDOCK docking protocol

HADDOCK uses a **3-step protocol** to dock two (or more) biomolecules using [[Ambiguous Interaction Restraint (AIR)|AIRs]] derived from experimental data:

**Step 1 — Rigid-body energy minimisation (EM)**:
- Both molecules treated as completely rigid.
- ~1,000 random starting orientations generated.
- Each pose energy-minimised under the HADDOCK scoring function.
- Best 200 poses selected for the next step.

**Step 2 — Semi-rigid simulated annealing in torsion-angle space (TAD-SA)**:
- Interface residues (active + passive) made **flexible** (backbone + side chains).
- Simulated annealing in torsion-angle space refines interface geometry.
- Allows limited induced fit at the binding interface without unfolding the proteins.

**Step 3 — Final refinement in Cartesian space with explicit water**:
- Short MD refinement in a shell of explicit TIP3P water.
- Relaxes steric clashes and optimises hydrogen bonding.
- Final [[HADDOCK scoring function|HADDOCK scores]] computed.

**Post-processing**: poses clustered by interface RMSD (~7.5 Å cutoff); clusters ranked by average HADDOCK score. Top-ranked cluster = predicted binding mode.

See [[molecular-docking]], [[Ambiguous Interaction Restraint (AIR)]], [[HADDOCK scoring function]].
