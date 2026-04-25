---
tags:
  - __DEFINITION
  - Module2
depth: 2
---
# Ambiguous Interaction Restraint (AIR)

The key input restraint in [[molecular-docking|HADDOCK]] docking. An AIR is an **ambiguous distance restraint** between the "active" and "passive" residues of two interacting molecules, derived from experimental data (NMR chemical shift perturbation, mutagenesis, cross-linking, etc.).

**Definitions**:
- **Active residues**: solvent-accessible residues experimentally shown to be at the interface.
- **Passive residues**: solvent-accessible neighbours of active residues (included to tolerate experimental noise).

**Effective distance formula**:

$$d_\text{eff} = \left(\sum_{i \in A,\, j \in B} \frac{1}{r_{ij}^6}\right)^{-1/6}$$

The restraint is satisfied when **any** atom pair (i from molecule A, j from molecule B) comes into contact — making it tolerant of positional ambiguity.

**Importance**: AIRs translate sparse biochemical knowledge (a few key interface residues) into structural restraints that guide docking without requiring complete atomic-level knowledge of the interface.

See [[molecular-docking]].
