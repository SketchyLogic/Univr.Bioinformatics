# Homology Modeling

**Summary**: Homology (comparative) modeling predicts the 3D structure of a target protein by using the known structure of a homologous protein (the template); accuracy depends heavily on the sequence identity between target and template.

**Sources**: [[Notes_Comp_Biology.pdf]]

**Last updated**: 2026-04-24

---

## The principle

Evolutionary related proteins share similar 3D structures. If a target protein shares sequence similarity with a protein of known structure (the template), the template's 3D coordinates can be used to construct a model for the target.

> "The quality of the predicted models is correlated with the evolutionary distance between the template and the target proteins." — Tramontano et al. (2008)

Homology modeling is the most reliable and accurate computational method for structure generation when experimental structures are absent.

## Sequence identity and model quality

| Sequence Identity | Expected quality |
|-------------------|-----------------|
| > 50% | High accuracy; model close to experimental structure |
| 30–50% | Good accuracy; local errors possible |
| < 30% (twilight zone) | Significant errors; SI < 20% → major problems |
| < 10% (midnight zone) | Statistically irrelevant similarity |

At SI < 50%, Cα RMSD from the true structure exceeds 1 Å. At SI < 30%, errors become severe and experimental restraints are strongly recommended to guide model building.

**Exception**: even very distant proteins can share structure if they belong to the same structural superfamily (e.g., GPCR proteins). The fold space has fewer distinct folds than the sequence space has families.

## Five categories of errors

(Fiser, 2010; Palomba & Cavasotto, 2015)

1. **Side-chain modeling errors** — incorrect positions of side chains, especially at buried residues involved in ligand binding.
2. **Structural deviations in correctly aligned regions** — the target may adopt a slightly different local conformation than the template even when the backbone alignment is correct.
3. **Inaccuracies from incorrect alignment** — especially at SI < 20%. Misaligned regions place residues incorrectly on the template fold.
4. **Distortions in misaligned regions** — when a region does not have an equivalent segment in the template (indels), residues may be placed incorrectly.
5. **Errors from incorrect or fragmentary templates** — using the wrong template (SI < 30%) or a fragment as template leads to misfolded models.

## Steps in model generation

### Step 1: Template search and target-template sequence alignment

The process of identifying suitable templates and aligning them to the target.

Three alignment methods (see [[sequence-alignment]]):
- **Pairwise** (BLAST, FASTA): for SI > 30%
- **Profile-sequence** (PSI-BLAST, HMMER): for twilight zone (10–30%)
- **Profile-profile** (HHpred): most sensitive; detects ~28% more superfamily relationships

Template search and alignment are often integrated in modern software.

### Step 2: Template selection

Once a list of suitable templates is found, at least five strategies exist (Tramontano et al., 2006):
1. Select the template with highest sequence similarity to the target
2. Build a "theoretical template" using the average coordinates of all possible templates
3. Take conformation from different templates for different regions (highest local similarity in each region)
4. Build a model from each template and select the best by model quality criteria
5. Derive spatial constraints from templates and satisfy them

### Step 3: Initial model construction

Three approaches:
- **Rigid body assembly** (SwissModel, RosettaCM, WHAT IF, COMPOSER): assembles a model from rigid bodies determined from the aligned 3D template
- **Segment matching** (SegMod/LEVITT): builds the crude model using a subset of atomic positions (Cα) from the 3D template
- **Satisfaction of spatial restraints** (MODELLER): extracts spatial constraints (distances, φ/ψ angles) from the template and minimises violations

### MODELLER (Fiser et al., 2000; Šali & Blundell, 1994)

The most widely used tool for homology modeling. Steps:
1. Align target sequence with template structure(s)
2. Extract spatial restraints (interatomic distances, backbone angles φ and ψ) from the experimentally solved template
3. Each restraint is associated with a probability density function (pdf)
4. Combine structural restraints with general spatial constraints from a CHARMM force field into an objective function
5. Minimise violations using variable target function method + MD with simulated annealing (SA)

### Step 4: Model refinement

- Correct local errors (side chains, loops, backbone)
- MD simulations can rearrange misfolded regions
- Multiple-template approaches improve accuracy by averaging errors

### Step 5: Model quality assessment

Three approaches:

#### Stereochemistry checks
- **PROCHECK** (Laskowski et al., 1993): validates bond lengths, angles, Ramachandran plot
- **WHATCHECK** (Hooft et al., 1996): comprehensive stereochemistry checks

#### Global quality estimation
- **DFIRE** (Zhou & Zhou, 2005): all-atom distance-dependent statistical potential
- **QMEAN** (Benkert et al., 2009): composite scoring function
- **DOPE** (Shen & Sali, 2006): statistical potential derived from ~1500 crystallographic structures

#### Local quality estimation (residue by residue)
- **ProQres** (Wallner & Elofsson, 2006): neural network predicting local 3D quality
- **ANOLEA** (Melo & Feytmans, 1998): statistical potential for packing quality
- **GROMOS** (Christen et al., 2005): empirical force field; calculates energy per residue

## When to use homology modeling

- Experimental structure of the target is unavailable or too expensive to obtain
- A template with >30% SI exists in the PDB
- For drug design or docking studies where a rough model is sufficient
- As a starting point for experimental structure determination (molecular replacement)

## Related pages

- [[sequence-alignment]]
- [[molecular-docking]]
- [[molecular-dynamics]]
- [[amino-acid-substitutions]]

## Other sources

- PDB (Protein Data Bank): source of all templates
- SwissModel server: automated homology modeling
- CASP (Critical Assessment of Structure Prediction): benchmark for structure prediction methods

## Test yourself

**Q**: What is the relationship between sequence identity and homology model quality?
**A**: Quality decreases with decreasing sequence identity. Above 50% SI, models are generally accurate. Below 30% (twilight zone) errors become significant. Below 20%, the alignment itself becomes unreliable, making the model potentially worse than no model. Cα RMSD > 1 Å is typical when SI < 50%.

**Q**: What are the five categories of errors in homology models?
**A**: (1) Side-chain modeling errors, (2) Structural deviations in correctly aligned regions, (3) Inaccuracies from misalignment, (4) Distortions in misaligned/indel regions, (5) Errors from incorrect or fragmentary templates.

**Q**: How does MODELLER build a homology model?
**A**: MODELLER extracts spatial restraints (interatomic distances, backbone dihedral angles φ and ψ) from the template structure, associates each with a probability density function, combines them with CHARMM force field constraints into an objective function, and minimises this function using a variable target function method followed by MD with simulated annealing.

**Q**: What is the twilight zone and why is it challenging for homology modeling?
**A**: The twilight zone (10–30% sequence identity) is where the statistical reliability of sequence homology becomes uncertain and alignments become error-prone. Models in this zone require experimental information (ligand binding data, mutagenesis) and careful manual curation to be trustworthy.
