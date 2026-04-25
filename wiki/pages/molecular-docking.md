# Molecular Docking

**Summary**: Molecular docking computationally predicts the preferred binding pose of a ligand (small molecule or protein) to a receptor by exploring conformational space and scoring interaction energy.

**Sources**: [[Notes_Comp_Biology.pdf]]

**Last updated**: 2026-04-24

---

## The problem

Proteins do not function in isolation — they interact with other proteins, nucleic acids, and small molecules. Predicting the **binding pose** (coordinates, orientation, conformation) of a ligand against a receptor is essential for understanding biological function and for drug design.

Formally: given two molecules (receptor + ligand), find the binding pose that minimises the interaction energy.

## State variables and search space

A ligand's binding pose is described by its **state variables**:
- Coordinates (x, y, z) of the binding site
- Orientation (rotational degrees of freedom)
- Internal conformation (torsional angles of rotatable bonds)

Each state variable represents one degree of freedom. The search space is the union of all possible state variable combinations.

## Two core components of any docking algorithm

1. **Scoring function**: evaluates the interaction energy of a given pose; used to rank poses.
2. **Search method**: explores the conformational space to find the best pose.

## Scoring functions

Empirical / force-field-based / knowledge-based scoring functions have been developed to approximate binding energy without full quantum mechanical calculation.

**Two types of search methods**:
- **Systematic**: samples the space at predefined intervals; deterministic; exhaustive but slow.
- **Stochastic**: makes random changes to state variables until a termination criterion is met. More efficient; not guaranteed to find the global minimum.

**Local vs. global search**:
- Local: finds nearest/local energy minimum.
- Global: searches the entire defined space for the global minimum.

## HADDOCK (Dominguez et al., 2003; Van Zundert et al., 2016)

The most successful information-driven docking software. Uses **experimental restraints** to predetermine the interaction surface, dramatically reducing the search space.

### Ambiguous Interaction Restraints (AIRs)

Experimental data (site-directed mutagenesis, NMR, bioinformatics predictions) define **active** and **passive** residues:
- **Active residues**: essential for interaction; must be at the interface.
- **Passive residues**: solvent-accessible surface neighbours of active residues.

An AIR defines an ambiguous intermolecular distance (d_iAB) with a maximum value of 3 Å between any atom of active residue i of molecule A and any atom of both active and passive residues of molecule B.

The effective distance is computed as:
$$d_{iAB}^{eff} = \left( \sum_{m_{iA}=1}^{N_{atoms}} \sum_{k=1}^{N_{res}B} \sum_{n_{kB}=1}^{N_{atoms}} \frac{1}{d_{m_{iA}n_{kB}}^6} \right)^{-1/6}$$

The 1/r⁶ sum ensures the restraint is satisfied as soon as any pair of atoms is in contact (mimics the attractive part of a Lennard-Jones potential).

### HADDOCK docking protocol (3 steps)

1. **Rigid body energy minimisation (EM)**: molecules are separated by ≥25 Å, rotated randomly, then subjected to rotational minimisation while maintaining rigid bodies.

2. **Semi-rigid simulated annealing in torsion angle space (TAD-SA)**: flexible SA in 4 stages (high-T rigid body, rigid body SA, semi-flexible SA with flexible side chains at interface, semi-flexible SA with fully flexible interface). Interface residues are defined by ±2 sequential amino acids around the active/passive residues.

3. **Final refinement in Cartesian space with explicit solvent**: structure is refined in an 8 Å shell of TIP3P water. No large structural changes expected; scoring improves.

### HADDOCK scoring

The **HADDOCK Score** (final):
```
FS = 1×Elec + 1×vdW + 1×Dsolv + 1×AIR
```

The **Rigid-body score** (after step 1):
```
RBS = 1×Elec + 1×vdW − 0.05×BSA + 1×Dsolv + 1×AIR
```

Where: Elec = electrostatics, vdW = van der Waals, Dsolv = desolvation, AIR = AIR restraint energy, BSA = buried surface area.

Results are clustered by RMSD (typically cut-off ~7 Å). A good model: low HADDOCK score AND belongs to a highly populated cluster.

**Caution**: the biologically active conformation in vivo is not necessarily the most energetically stable in isolation. The frequency of a cluster AND its energy should both be considered.

### Interface prediction (for when experimental data are absent)

CPORT (de Vries & Bonvin, 2011): consensus predictor combining 6 interface prediction methods (WHISCY, PIER, ProMate, cons-PPISP, SPPIDER, PINUP) to define active/passive residues for use in HADDOCK.

## Autodock suite (Morris et al., 2009; Trott & Olson, 2010)

Two popular programs:

### Autodock (Morris et al., 2009)
- Empirical free-energy force field + rapid Lamarckian genetic algorithm search
- Includes explicit polar hydrogen and electrostatic/hydrogen bond terms
- Steps: (1) prepare receptor .pdbqt, (2) prepare ligand .pdbqt, (3) generate grid, (4) generate maps via AutoGrid4, (5) generate docking parameters, (6) run Autodock, (7) analyse results with ADT

### Vina (Trott & Olson, 2010)
- Simpler scoring function (gradient-optimised; no electrostatic term, no explicit H atoms)
- Faster than Autodock; good results for ligands of typical biological size
- Input: receptor + ligand .pdbqt + conf.txt (search space dimensions)
- Output: up to 10 binding poses with estimated free energy of binding

Both use stochastic search; poses are clustered spatially for consistency assessment. The receptor molecule is kept rigid (largest approximation in both protocols).

## LeapFrog / Sybyl

LeapFrog (Tripos Inc., component of Sybyl v7.3) screens a virtual library of ligands/functional monomers against a receptor binding site. Uses two-stage scoring:
1. Monomer-template complexation
2. Scoring complementarities between monomer and template (site-point matching)

Parameters optimised to favour hydrogen bonding; places less weight on hydrophobic/π-π interactions.

## Comparison: HADDOCK vs. Autodock/Vina

| Aspect | HADDOCK | Autodock/Vina |
|--------|---------|---------------|
| Input | Experimental restraints (AIRs) | Geometry of binding site |
| Flexibility | Receptor interface residues flexible | Receptor rigid |
| Intended use | Protein-protein/protein-ligand with known interaction data | Small molecule docking, virtual screening |
| Output | Clustered structures with HADDOCK score | Poses with estimated ΔG binding |

## Related pages

- [[homology-modeling]]
- [[molecular-dynamics]]
- [[sequence-alignment]]

## Other sources

- Morris et al. (1998) — docking and virtual screening textbook
- Van Zundert et al. (2016) — HADDOCK 2.2
- Trott & Olson (2010) — Vina paper

## Test yourself

**Q**: What are the two core components shared by all docking algorithms?
**A**: (1) A **scoring function** that evaluates the quality of a pose (interaction energy), and (2) a **search method** that explores conformational space to find the best pose.

**Q**: What is an AIR in HADDOCK, and what experimental data defines it?
**A**: An Ambiguous Interaction Restraint is a distance restraint between active/passive residues of two interacting molecules. It is defined from experimental data such as site-directed mutagenesis, NMR chemical shift perturbations, or bioinformatics interface predictions.

**Q**: What are the three steps of the HADDOCK docking protocol?
**A**: (1) Rigid body energy minimisation, (2) Semi-rigid simulated annealing in torsion angle space (TAD-SA), (3) Final refinement in Cartesian space with explicit solvent (8 Å TIP3P water shell).

**Q**: What is the main difference between Autodock and Vina?
**A**: Autodock uses an empirical free-energy force field with a Lamarckian genetic algorithm and includes explicit electrostatic and hydrogen bond terms. Vina uses a simpler gradient-optimised scoring function without explicit electrostatics, making it faster but less accurate for some cases.
