---
tags:
  - __DEFINITION
  - Module2
---
# Periodic boundary conditions (PBC)

A technique used in [[molecular-dynamics|molecular dynamics]] simulations to eliminate surface artifacts when simulating a **finite box** of atoms. The simulation box is surrounded by infinite periodic copies of itself — when an atom exits one face of the box, it re-enters from the opposite face.

**Why PBC is needed**: without it, atoms at the surface experience a vacuum boundary with no neighbours on one side. PBC effectively simulates a **bulk (infinite) system** using a manageable number of atoms.

**Minimum image convention**: each atom interacts with the **nearest image** of every other atom (including periodic copies). This requires the box to be large enough that a molecule does not interact with its own periodic image.

**Practical rule**: add ≥ 1–2 nm of solvent padding around the solute on each side to prevent self-interaction across periodic boundaries.

**Commonly used box shapes**: cubic, rhombic dodecahedron, truncated octahedron (the latter two are more space-efficient for globular proteins).

See [[molecular-dynamics]], [[Explicit vs. implicit solvent]].

# TLDR
Wrap the simulation box so any atom leaving one face immediately re-enters from the opposite face — effectively simulating a bulk infinite system with a small number of atoms.
