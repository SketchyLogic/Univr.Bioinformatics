---
tags:
  - __DEFINITION
  - Module2
---
# Force field

A mathematical model of the **potential energy of a molecular system** as a function of atomic positions. Used in [[molecular-dynamics|molecular dynamics]] (MD) simulations, energy minimisation, and [[Spatial restraints|MODELLER restraint-based modeling]].

**Two classes of terms**:

**Bonded interactions** (local geometry):
- Bond stretching: harmonic potential U = ½k_b(r − r₀)²
- Angle bending: harmonic potential U = ½k_θ(θ − θ₀)²
- Dihedral (torsional) angles: periodic potential
- Improper dihedrals: maintain chirality and planarity

**Non-bonded interactions** (long-range):
- Electrostatics: Coulomb potential U = q₁q₂/(4πεr)
- Van der Waals: Lennard-Jones potential U = ε[(σ/r)¹² − (σ/r)⁶]

**Common force fields**: AMBER (proteins, nucleic acids), CHARMM (biomolecules, used in MODELLER), GROMOS (united-atom, efficient), OPLS (organic molecules), MARTINI (coarse-grained).

Parameters are derived from quantum mechanics calculations and experimental thermodynamic data.

See [[molecular-dynamics]], [[modeller]].
