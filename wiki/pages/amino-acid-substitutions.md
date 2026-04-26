---
CreatedAt: 2026-04-24
LastUpdateAt: 2026-04-24
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedById: claude-sonnet-4-6
---
# Amino Acid Substitutions and Protein Function

**Summary**: Nonsynonymous SNPs (nsSNPs) cause amino acid changes in proteins; computational prediction methods (SIFT, PolyPhen, SNPs3D, etc.) use evolutionary conservation and/or 3D structure to classify substitutions as damaging or neutral.

**Sources**: [[annurev.genom.7.Ng_Henikoff.pdf]]

**Last updated**: 2026-04-24

---

## Background: nsSNPs and their impact

A **nonsynonymous (missense) SNP (nsSNP)** is a single base change in a coding region that causes an amino acid change in the corresponding protein. Because amino acid changes can affect protein function, nsSNPs have the largest impact on human health compared to SNPs in non-coding regions.

Scale of the problem:
- 67,000–200,000 common nsSNPs in the human population
- Each person is heterozygous for ~24,000–40,000 nsSNPs
- ~25–30% of nsSNPs are predicted to negatively affect protein function by most methods

Experimentally characterising each nsSNP's effect is expensive and time-consuming. **Amino acid substitution (AAS) prediction methods** use computational approaches to prioritise nsSNPs for experimental follow-up.

## The two core biological observations

1. **Conservation**: mutations that affect protein function tend to occur at **evolutionarily conserved** positions. Disease-causing mutations are overrepresented at conserved sites.

2. **Structure**: mutations that affect protein function tend to occur at **buried** (not surface-exposed) positions in the 3D structure. Buried positions are typically important for structural integrity or active site geometry.

These observations are the basis of all AAS prediction methods.

## General prediction workflow

```
Input: protein sequence + amino acid substitution (AAS)
           |
     ┌─────┴──────────────────┐
  Sequence              Structure
  alignment             database
     |                     |
  PSSM from             Assess structural
  homologs              features (SA,
     |                  B-factor, etc.)
     └──────────────────────┘
           |
     Apply scoring rules
           |
  Output: damaging / tolerated
```

(Flowchart from Ng & Henikoff 2006, Figure 2)

## Sequence-based methods

### SIFT (Sorting Intolerant From Tolerant)
Ng & Henikoff (2001–2003).

1. Collect homologous sequences by searching a protein sequence database
2. Build a multiple sequence alignment (MSA)
3. Compute a PSSM (position-specific scoring matrix) from the alignment
4. For the substituted position: look up the probability of observing the new amino acid. 
   - Score < 0.05 → **damaging** (intolerant)
   - Score ≥ 0.05 → **tolerated**

Key insight: if an amino acid has never (or rarely) appeared at a position across all homologs, the position cannot tolerate that amino acid — any substitution there is likely to be deleterious.

**Practical note**: using **orthologs** (same gene, different species) rather than paralogs gives ~8% better accuracy. Paralogs may have different functions, introducing noise.

**Limitation**: does not use structural information; may miss surface substitutions that disrupt intermolecular interactions (e.g., β-globin E6V is surface-exposed and predicted tolerated by SIFT, but correctly predicted damaging because the position is conserved).

### PANTHER PSEC
Uses hidden Markov model (HMM) family profiles (PANTHER HMM families) to compute conservation scores. A negative score is damaging; positive is gain-of-function.

## Structure-based methods

### SNPs3D (Yue & Moult, 2006)
- Structure-based SVM: uses 15 structural features
- Sequence-based SVM: uses 5 sequence conservation features
- Score < 0 → damaging on protein structure

Coverage: structure-based ~14%, sequence-based ~71%. Structure-based methods are limited by the availability of 3D structures (~14% of nsSNPs have a structure).

### TopoSNP
Classifies substitutions as buried, surface, or in a pocket. Also provides conservation scores from Pfam alignments.

## Combined (sequence + structure) methods

### PolyPhen (Polymorphism Phenotyping)
Uses sequence conservation + structure + Swiss-Prot functional annotation:
- Models position of AAS using Swiss-Prot annotations (active site, binding site, disulfide bond)
- Incorporates solvent accessibility, B-factor from crystal structure
- Coverage: up to 81% (sequence-based component high)

Limitation: use of Swiss-Prot functional annotation reduces false negatives by 1.6% but **increases false positives by 2.1%**. Caution when annotation alone predicts damaging.

### PMUT
Two neural networks using internal databases, secondary structure prediction, and sequence conservation. When structure is included: FN error 12%, FP error 10%.

## Performance comparison (from Table 1, Ng & Henikoff 2006)

| Method | FN error | FP error | Coverage | Algorithm |
|--------|----------|----------|---------|-----------|
| SIFT | 31% | 20% | 60% | PSSM + Dirichlet priors |
| PolyPhen | 31% | 9% | 81% | Conservation + structure + annotation |
| SNPs3D (seq) | 20% | 10% | 71% | SVM (5 conservation features) |
| SNPs3D (struct) | 26% | 15% | 14% | SVM (15 structural factors) |
| PANTHER PSEC | 59% | N/A | 40% | PANTHER HMM |
| PMUT | 21% | 17% | 60% | Neural network |
| TopoSNP | 12% | N/A | 68% | Position classification + conservation |

FN = false negative (predicted neutral when damaging); FP = false positive (predicted damaging when neutral).

## Applications

### Mendelian disease
AAS methods predict 70–90% of AASs in disease databases (OMIM, HGMD, Swiss-Prot) as damaging, vs. only 10–20% in neutral sets. This demonstrates strong discriminatory power for identifying causative mutations.

### Complex disease and population genetics
nsSNPs with low minor allele frequency (<6%) are predicted damaging by SIFT twice as often as common nsSNPs (>10%). This is evidence that **damaging nsSNPs are under purifying selection** — they are rare because natural selection removes them.

### Drug design and pharmacogenomics
Predicting which nsSNPs affect drug-metabolising enzymes or drug targets helps personalise treatment.

## Key caveats

### Structure-based caveat
- Protein structures are usually determined in isolated crystal form → cannot capture supramolecular interactions
- Structure-based methods tend to predict surface positions as neutral — but surface positions may be important for intermolecular contacts
- Classic example: β-globin E6V (sickle cell) is surface-exposed → structure-based PolyPhen predicts **tolerated**, but sequence-based SIFT correctly predicts **damaging** because the position is conserved

### Sequence-based caveat
- Choice of homologous sequences critically affects the PSSM
- Using orthologs (same gene in different species) > paralogs
- Proteins under positive selection may have "conserved" positions that have actually changed functionally

### General caveat
- These are **predictions**, not diagnoses. They are meant to prioritise experiments, not replace them.
- AAS methods predict ~25–30% of nsSNPs as damaging — these have lower minor allele frequency, confirming the prediction reflects real selection

## Related pages

- [[evolutionary-conservation]]
- [[sequence-alignment]]
- [[homology-modeling]]

## Other sources

- Ng & Henikoff (2006) Annual Review of Genomics & Human Genetics
- dbSNP database (NCBI): repository of known nsSNPs
- OMIM, HGMD, Swiss-Prot: disease mutation databases
- SIFT web server; PolyPhen-2 server

## Test yourself

**Q**: What are the two biological observations underlying all AAS prediction methods?
**A**: (1) Mutations that affect protein function tend to occur at **evolutionarily conserved** positions. (2) Mutations that affect function tend to occur at **buried** (structurally important) positions. These are the basis of sequence-based and structure-based methods respectively.

**Q**: How does SIFT predict whether an amino acid substitution is tolerated or damaging?
**A**: SIFT aligns the protein to homologs, builds a PSSM, and looks up the probability of the new amino acid at the substituted position. If the probability is below 0.05 (the amino acid is very rare in the alignment column), the substitution is predicted **damaging**.

**Q**: Why is coverage lower for structure-based than sequence-based AAS methods?
**A**: Because protein 3D structures are far less available than sequences. Structure-based methods can only make predictions for proteins with solved structures or reliable homology models (sequence identity > 40%). Coverage is ~14% for structure-only methods vs. up to 81% for sequence-based methods.

**Q**: What does it mean that nsSNPs with low minor allele frequency are more often predicted damaging?
**A**: It is evidence that **damaging nsSNPs are under purifying selection** — mutations that disrupt protein function reduce fitness and are therefore maintained at low frequency in the population. The AAS prediction methods capture this evolutionary signal.

**Q**: Why is β-globin E6V a classic example of the limitation of structure-based methods?
**A**: E6V is a surface-exposed substitution. Structure-based methods tend to predict surface substitutions as neutral (because buried positions are more critical for structural stability). But E6V causes sickle cell anemia because it promotes hemoglobin aggregation via intermolecular contacts — interactions invisible in the single-protein crystal structure. Sequence-based SIFT correctly predicts it as damaging because the position is conserved.
