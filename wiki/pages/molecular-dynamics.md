# Molecular Dynamics

**Summary**: Molecular dynamics (MD) is a computer simulation technique that models the time evolution of a system of interacting atoms by numerically integrating Newton's equations of motion; it captures the dynamical behaviour of biomolecules.

**Sources**: [[Notes_Comp_Biology.pdf]]

**Last updated**: 2026-04-24

---

## What is MD and why do we need it?

Homology modeling and docking produce **static** 3D structures. Biological processes happen in **time** — protein folding, ligand binding/unbinding, conformational changes, membrane dynamics. MD provides a method to simulate these dynamics.

**Definition**: a computer simulation approach where the time evolution of a set of interacting atoms is followed by integrating (at discrete timesteps) their equations of motion.

## Levels of detail

Biological processes span time scales from femtoseconds (bond vibrations) to seconds (protein folding, signalling), and length scales from picometres (bond lengths) to micrometres (cellular structures). No single method covers all scales.

| Method | Resolution | Accessible timescale | Atoms |
|--------|------------|---------------------|-------|
| Quantum mechanics (QM) / ab initio | Electronic | fs | ~100 |
| Hybrid QM/MM | Mixed | fs–ps | ~1000 |
| Atomistic Molecular Mechanics (MM) | All atoms | ps–μs | ~10⁶ |
| Coarse-grained (CG) | Bead model | ns–ms | ~10⁸ |
| Mesoscale / finite elements | Continuum | ms+ | Large |

The choice of method must match the timescale and length scale of the biological process under investigation.

## The force field

A **force field** is a mathematical description of the forces governing interactions between atoms. It defines:

**Bonded interactions** (involving 2, 3, or 4 atoms):
- Bond stretching (harmonic potential)
- Angle bending
- Dihedral (torsional) angles
- Improper dihedrals (for planarity)

**Non-bonded interactions** (2 atoms):
- Electrostatic (Coulomb)
- Van der Waals (Lennard-Jones or Morse potential)

The force field does not include electronic structure — it implicitly represents electrons through parameterised interactions. This means MM cannot model chemical reactions (bond making/breaking).

### Major force fields

| Force field | Notes |
|------------|-------|
| AMBER | Ab initio QM-derived parameters; explicit polar hydrogens |
| GROMOS | United atom (non-polar H implicit); parameterised to reproduce hydration/solvation free enthalpies |
| CHARMM | Widely used for proteins and nucleic acids |
| OPLS | Jorgensen et al. 1996; popular for small molecules |
| MARTINI | Coarse-grained force field (4 MM atoms = 1 CG bead) |

**Important**: different force fields cannot be mixed in the same simulation — their parameters are internally consistent and not cross-compatible.

## The MD algorithm

Given a system of N particles with positions {xᵢ}:

1. **Calculate energy**: U({xᵢ}) from the force field
2. **Calculate forces**: Fᵢ = −∂U/∂xᵢ
3. **Calculate accelerations**: aᵢ = Fᵢ/mᵢ (Newton's 2nd law)
4. **Integrate equations of motion**: update velocities and positions at each timestep
5. Output **trajectory** (positions, velocities, forces at each timestep)
6. Return to step 1

The trajectory is the primary output: a time series of atomic positions from which thermodynamic observables are computed.

## The timestep

The timestep Δt must be small enough to accurately integrate the fastest motions:
- Fastest motions: bond stretching/bending vibrations → period ~10 fs → Δt ≤ 1–4 fs
- Larger Δt: coarser integration, potential instability and artefacts
- Smaller Δt: more accurate but higher computational cost

## Integration algorithms

The integrator must be **time-reversible** and **symplectic** (preserves phase space volume, obeying Liouville's theorem).

| Algorithm | Notes |
|-----------|-------|
| Verlet (1967) | Classic; numerically stable |
| Velocity Verlet (Verlet 1968; Swope et al. 1982) | More numerically precise; explicitly tracks velocities |
| Leapfrog (Hockney & Eastwood 1988) | Computationally efficient; positions and velocities staggered by Δt/2 |

## Periodic Boundary Conditions (PBC)

The simulated system is finite; without boundary treatment, edge atoms experience an artificial vacuum. Two approaches:

- **Hard walls**: unphysical; creates surface effects
- **PBC** (standard): the simulation box is replicated infinitely in all directions. Atoms leaving one side re-enter from the opposite side. The box corresponds to the 3D surface of a 4-torus.

The box shape (cube, parallelpiped, rhombic dodecahedron) must minimise holes. The system must be electrically neutral for PBC electrostatics. The box should be large enough that the molecule does not interact with its periodic image.

## Solvation

Biomolecules function in aqueous solution. Two approaches:

### Explicit solvent
Individual water molecules are simulated. More accurate but slower.
- Common water models: SPC/E, TIP3P (3-point), TIP4P (4-point — better approximates charge distribution)
- Water models generally overestimate diffusion and underestimate internal structure compared to real water

### Implicit solvent
Solvent modelled as a continuum dielectric. Faster; lower accuracy.
- Polar component: continuous dielectric (Poisson-Boltzmann or Generalised Born)
- Nonpolar component: estimated from solvent-accessible surface area (SASA)

## Cut-off methods for non-bonded interactions

Non-bonded interactions (electrostatics, vdW) grow quadratically with atom count. For 10,000 atoms, ~50 million pairwise interactions. Beyond a cut-off distance, interactions are neglected or treated approximately.

Three approaches:
1. **Truncation**: interactions zeroed beyond cut-off. Simple but introduces artefacts.
2. **Shift**: modifies potential to reach zero smoothly at cut-off.
3. **Switch**: reduces potential to zero over a predefined distance range.

## Thermostats

Newton's equations conserve total energy → **microcanonical (NVE) ensemble**. Biological conditions require **NVT** (constant temperature) or **NPT** (constant temperature and pressure) ensembles. A thermostat couples the system to a heat bath:
- **Velocity rescaling** (simple but artificial — erases thermal fluctuations)
- **Nosé-Hoover thermostat**: generates canonical ensemble
- **Berendsen thermostat**: fast equilibration; not strictly canonical
- **V-rescale**: stochastic velocity rescaling; correct canonical ensemble

## Coarse-grained methods

Atomistic MD is too slow for many biologically relevant timescales. CG methods reduce multiple atoms to single "beads":

### MARTINI force field (Monticelli et al., 2008)
- Mapping: 4 MM atoms = 1 CG bead
- Non-bonded parameters: Lennard-Jones potentials reproducing oil/water partition coefficients
- Bonded parameters: from statistical polypeptide properties (PDB database)
- Electrostatics: treated explicitly
- Secondary structure must be set up and restrained at the start (not self-organising)
- Best suited for: protein-lipid membrane simulations, lipid bilayers, large-scale assembly

GROMACS (Pronk et al. 2013) supports both MM and CG representations; the difference is only in the force field used.

## Major MD software

| Software | Notes |
|---------|-------|
| GROMACS | Open source; very fast; supports MM and CG |
| AMBER | Widely used for biomolecules; good force fields |
| CHARMM | Comprehensive; strong in method development |
| NAMD | High-performance parallel MD |

## Related pages

- [[homology-modeling]]
- [[molecular-docking]]

## Other sources

- Frenkel & Smit *Understanding Molecular Simulation* (2002)
- Cascella & Vanni (2015) — time/length scale overview figure
- GROMACS manual and tutorials

## Test yourself

**Q**: What is the ergodic hypothesis in MD, and why is it important?
**A**: The ergodic hypothesis states that if a system is allowed to evolve for infinite time, it will pass through all possible states. This means the time average of an observable from a long MD simulation equals the ensemble average. In practice, convergence is assessed when observables stop changing in time.

**Q**: Why is the timestep restricted to 1–4 fs in typical MD simulations?
**A**: Because bond stretching and bending vibrations occur on timescales of ~10 fs. To accurately integrate these fastest motions, the timestep must be smaller than half the characteristic time of the fastest vibration (Nyquist criterion). Larger timesteps cause numerical instability.

**Q**: What is the key difference between explicit and implicit solvent in MD?
**A**: Explicit solvent includes individual water molecules; it is more accurate (captures hydration shell, water dynamics) but much slower due to the increased number of atoms. Implicit solvent models water as a continuous dielectric, reducing computational cost at the expense of accuracy.

**Q**: What is the MARTINI force field and what is its mapping strategy?
**A**: MARTINI is a coarse-grained force field where 4 heavy atoms (MM level) are grouped into 1 CG bead. Non-bonded parameters reproduce oil/water partition coefficients. Bonded parameters come from statistical properties of polypeptides from the PDB. It is widely used for protein-lipid and membrane simulations.
