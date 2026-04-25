---
tags:
  - __DEFINITION
  - Module2
---
# Ergodic hypothesis

A foundational assumption in [[molecular-dynamics|molecular dynamics]] (MD) simulations: **given infinite simulation time, a system will sample all accessible states of phase space**. Therefore:

> **time average = ensemble average**

**Practical consequence**: a sufficiently long MD trajectory can be used to compute thermodynamic observables (free energies, binding affinities, heat capacities) as time averages without running many independent simulations.

**Convergence check**: assess ergodicity by verifying that observables (e.g., RMSD, Rg, energy) have stabilised over time and show no systematic drift.

**Limitation**: MD trajectories are rarely truly ergodic on accessible timescales — systems can get trapped in local energy minima, especially for large conformational changes or protein folding. Methods like replica exchange MD (REMD), metadynamics, or umbrella sampling are used to improve sampling when ergodicity is suspected to be violated.

See [[molecular-dynamics]].
