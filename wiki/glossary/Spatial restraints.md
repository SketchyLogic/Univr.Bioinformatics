---
tags:
  - __CONCEPT
  - Module2
---
# Spatial restraints

The core mechanism by which [[modeller|MODELLER]] builds a [[Homology modeling|homology model]]. Spatial restraints are geometric constraints on the **target protein** derived from template structure(s) and prior knowledge.

**Types extracted from the template**:
- **Interatomic distance restraints**: Cα–Cα, Cβ–Cβ, main-chain N–O distances (observed in template → applied to target)
- **Backbone dihedral angle restraints**: φ, ψ angles derived from Ramachandran statistics for each residue type and secondary structure environment
- **Stereochemical restraints**: from the CHARMM force field (ideal bond lengths, bond angles, planarity of peptide bonds)

**Objective function**: all restraints are expressed as **probability density functions (PDFs)**; their combined negative log-probability forms the objective function that MODELLER minimises.

**Optimisation**: the objective function is minimised first by the Variable Target Function (VTF) method, then refined by molecular dynamics with simulated annealing (MD/SA).

See [[modeller]], [[homology-modeling]].
