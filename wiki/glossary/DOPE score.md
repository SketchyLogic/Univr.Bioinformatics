---
tags:
  - __DEFINITION
  - Module2
---
# DOPE score

**Discrete Optimized Protein Energy** — a statistical potential used in [[modeller|MODELLER]] to assess the quality of a [[Homology modeling|homology model]].

**How it's computed**: derived from a statistical analysis of inter-residue distances in a reference set of high-resolution crystal structures from the PDB. For each atom-pair type (e.g., Cα–Cα), the observed distance distribution is compared to a reference state, giving an energy-like score via the inverse Boltzmann relationship.

**Interpretation**: a **more negative** DOPE score indicates a better model. Uses:
1. Select the best model among multiple MODELLER runs (generate 10–100 models, pick the lowest DOPE).
2. Identify poorly modeled regions via the **residue-by-residue DOPE profile** (peaks indicate problem areas such as loops).

**Limitation**: a statistical potential, not a physical force field. Better for **ranking models** than for absolute quality assessment. Should be complemented with Ramachandran plot analysis and PROCHECK/WHATCHECK stereochemistry checks.

See [[modeller]], [[homology-modeling]].
