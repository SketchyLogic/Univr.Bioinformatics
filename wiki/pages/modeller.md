---
CreatedAt: 2026-04-25
LastUpdateAt: 2026-04-25
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedById: claude-sonnet-4-6
---
# MODELLER

**Summary**: MODELLER is the most widely used tool for homology modeling; it builds protein 3D models by extracting spatial restraints from a template structure and minimising violations using molecular dynamics with simulated annealing.

**Sources**: [[Notes_Comp_Biology.pdf]]

**Last updated**: 2026-04-25

---

## Overview

MODELLER (Šali & Blundell, 1994; Fiser et al., 2000) implements the **satisfaction of spatial restraints** approach to [[homology-modeling]]. Rather than assembling rigid template fragments, it extracts interatomic distance and angle constraints from the template and treats model building as a constraint-satisfaction problem solved by energy minimisation.

It is the standard tool in the field: used in academic pipelines, automated servers (ModBase, ModWeb), and as a starting point for drug discovery and structural biology.

## Core concept: spatial restraints

Given a target-template alignment:
1. For each pair of equivalent residues, extract **interatomic distances** (Cβ–Cβ, Cα–Cα, N–O hydrogen bonds) from the template structure.
2. For each aligned residue, extract **backbone dihedral angles** (φ, ψ) from the template.
3. Express each restraint as a **probability density function (PDF)**:
   - Distance restraints: a Gaussian (or sum of Gaussians) centred on the template distance.
   - Dihedral restraints: periodic functions centred on the template angles.

The PDFs encode: *the target value is most likely close to the template value, with uncertainty that increases with evolutionary distance.*

## Objective function

All spatial restraints plus general **CHARMM force field** terms (bond lengths, bond angles, non-bonded contacts) are combined into a single objective function (a negative log-likelihood):

```
F = Σ (restraints from template) + Σ (CHARMM terms)
```

The goal is to find atomic coordinates of the target that **minimise F** — satisfying template-derived restraints while maintaining physically plausible geometry.

## Optimisation strategy

Minimisation is performed in two stages:

1. **Variable Target Function (VTF) method**: starts with only short-range restraints, progressively adding longer-range ones. This avoids getting trapped in early local minima.

2. **Molecular Dynamics with Simulated Annealing (MD/SA)**: high-temperature MD allows the chain to escape local minima; slow cooling finds a low-energy minimum.

The process is stochastic — running MODELLER multiple times produces an ensemble of models. The best model is selected by the **DOPE score**.

## Workflow

```
Input: target sequence + template PDB file + target-template alignment
         |
1. Extract spatial restraints from template
         |
2. Build initial model from template coordinates
         |
3. Optimise with VTF + MD/SA
         |
4. Repeat N times (typically 5–50 models)
         |
5. Select model with lowest DOPE score
         |
Output: PDB file of best model
```

## Quality assessment

| Tool | What it checks |
|------|---------------|
| DOPE | Statistical potential; global model quality (lower = better) |
| PROCHECK | Stereochemistry: bond lengths, angles, Ramachandran plot |
| WHATCHECK | Comprehensive stereochemistry checks |
| QMEAN | Composite Z-score calibrated against crystal structures |
| ProQres | Per-residue local quality estimation (neural network) |

Good practice: generate ≥ 5 models, select by DOPE, then inspect the Ramachandran plot with PROCHECK.

## Multiple templates

MODELLER natively supports **multiple templates**: restraints from all aligned templates are combined into the objective function. Errors in different templates tend to be uncorrelated, so the model averages out template-specific artefacts. Multiple-template modeling is strongly recommended when:
- No single template has SI > 50%.
- Different regions of the target are covered by different templates.
- Templates differ in loop conformation.

## Practical considerations

| SI range | Expected model quality | Practical implication |
|----------|----------------------|----------------------|
| > 50% | High; near-experimental | Reliable for docking, virtual screening |
| 30–50% | Good; local errors possible | Refine loops before docking |
| < 30% (twilight zone) | Significant errors | Use multiple templates; consider experimental restraints |
| < 20% | Major errors; alignment unreliable | Switch to HHpred for alignment; validate extensively |

At SI < 30%, inspect the target-template alignment manually. Use `modeller.LoopModel` to refine loop regions corresponding to insertions/deletions relative to the template.

## Comparison with other modeling approaches

| Approach | Example tools | Principle |
|----------|--------------|-----------|
| Rigid body assembly | SwissModel, COMPOSER | Assemble template fragments as rigid blocks |
| Segment matching | SegMod | Match Cα positions to template |
| **Spatial restraints** | **MODELLER** | Restraint satisfaction + MD/SA |

MODELLER is more flexible than rigid-body methods: it handles multiple templates, loop insertions, and non-standard residues in a unified framework.

## Related pages

- [[homology-modeling]]
- [[sequence-alignment]]
- [[sequence-search-tools]]
- [[molecular-dynamics]]
- [[molecular-docking]]

## Other sources

- Šali A. & Blundell TL. (1994) — original MODELLER paper. *J. Mol. Biol.* 234:779–815
- Fiser A., Do RK. & Šali A. (2000) — Modeling of loops. *Protein Science* 9:1753–1773
- Shen MY. & Šali A. (2006) — DOPE statistical potential. *Protein Science* 15:2507–2524
- ModBase: database of comparative protein structure models (modbase.compbio.ucsf.edu)
- MODELLER manual: https://salilab.org/modeller/manual/

## Test yourself

**Q**: What are "spatial restraints" in MODELLER and where do they come from?
**A**: Spatial restraints are probabilistic constraints on interatomic distances (Cβ–Cβ, Cα–Cα) and backbone dihedral angles (φ, ψ) extracted from the aligned template structure. Each is expressed as a probability density function centred on the observed template value. They encode the expectation that the target structure is similar to the template, with uncertainty that scales with evolutionary distance.

**Q**: Why does MODELLER run multiple models and select by DOPE score?
**A**: The MD/SA optimisation is stochastic — different runs explore different parts of the conformational landscape. Running multiple models increases the chance of finding the global minimum. DOPE is a statistical potential estimating model quality; the lowest-DOPE model is the best approximation of the true structure.

**Q**: What is the advantage of using multiple templates in MODELLER?
**A**: Errors from individual templates tend to be uncorrelated. By combining restraints from several templates, MODELLER averages out template-specific artefacts — particularly useful when no single template has SI > 50%.

**Q**: At what sequence identity does MODELLER become unreliable, and what can help?
**A**: Below 30% SI (twilight zone) errors become significant; below 20% the alignment itself is unreliable. Strategies: use HHpred for the alignment (more sensitive than BLAST/PSI-BLAST), use multiple templates, run loop modelling (`modeller.LoopModel`) on insertions, and validate with PROCHECK and QMEAN.
