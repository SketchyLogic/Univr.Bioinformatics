---
tags:
  - __DEFINITION
  - Module2
---
# Cα RMSD

**Root Mean Square Deviation of alpha-carbon positions** — the standard metric for measuring structural similarity between two protein structures (or a homology model and its reference).

**Formula**: RMSD = √( (1/N) Σᵢ |rᵢ − r′ᵢ|² )  
where rᵢ and r′ᵢ are the 3D coordinates of the i-th Cα atom in the two structures after **optimal superposition** (minimising RMSD over all rotations and translations).

**Typical values in homology modeling**:

| Sequence identity | Expected Cα RMSD |
|-------------------|-----------------|
| > 50% | ~1 Å |
| 30–50% | ~1.5–2 Å |
| 10–30% (twilight) | ~3–5+ Å |

**Limitation**: RMSD is a **global** measure. Flexible loops or disordered termini can dominate the score while the core fold is well-modeled. For functional assessment, check the active site RMSD separately.

See [[homology-modeling]], [[modeller]], [[Sequence identity zones]].
