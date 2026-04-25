---
tags:
  - __DEFINITION
  - Module2
---
# MARTINI coarse-grained force field

A coarse-grained (CG) [[Force field|force field]] that reduces computational cost by representing groups of atoms as single interaction **beads**.

**Mapping rule**: approximately **4 heavy atoms → 1 CG bead** (4:1 mapping).

**Parameter fitting**:
- Non-bonded Lennard-Jones parameters: calibrated to reproduce **oil/water partition coefficients** (thermodynamic data, not structural fitting).
- Bonded parameters: derived from statistical analysis of protein backbone geometry in the PDB.
- Electrostatics: treated explicitly at the CG level.

**Key advantage**: ~100–1000× speed-up over all-atom MD, enabling microsecond-to-millisecond timescale simulations of large systems.

**Main applications**: protein-lipid membrane simulations, large protein complexes, polymer self-assembly, vesicle formation.

**Trade-off**: loss of atomic detail; cannot capture processes requiring sub-Å resolution (enzyme mechanisms, precise ligand binding poses, protonation effects).

See [[molecular-dynamics]].
