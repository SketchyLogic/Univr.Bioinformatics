---
tags:
  - __CONCEPT
  - Module2
---
# Explicit vs. implicit solvent

Two strategies for handling the aqueous environment in [[molecular-dynamics|molecular dynamics]] (MD) simulations:

| | Explicit solvent | Implicit solvent |
|---|---|---|
| **Model** | Individual water molecules (SPC/E, TIP3P, TIP4P) simulated as atoms | Solvent replaced by a continuum dielectric (GB, PB, or SASA models) |
| **Accuracy** | High — captures hydration shells, water dynamics, water-mediated H-bonds | Lower — misses specific water effects and entropic contributions from water ordering |
| **Speed** | Slow — water molecules often outnumber protein atoms 5–10:1 | Fast — no solvent atoms to integrate |
| **Requires PBC?** | Yes (to avoid surface effects) | No |
| **Best for** | Binding thermodynamics, membrane simulations, detailed dynamics | Large-scale conformational sampling, protein folding studies |

**Most common MD practice**: explicit solvent with [[Periodic boundary conditions (PBC)|PBC]] and TIP3P or SPC/E water model. 

[[molecular-docking|HADDOCK]] uses explicit water in its final refinement step. [[modeller|MODELLER]] uses the CHARMM force field without explicit solvent for model building. See [[molecular-dynamics]].
