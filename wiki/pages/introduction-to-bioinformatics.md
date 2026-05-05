---
CreatedAt: 2026-05-02
LastUpdateAt: 2026-05-02
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedById: claude-sonnet-4-6
---

# Introduction to Bioinformatics

**Summary**: Bioinformatics is the scientific discipline that solves biological problems at the molecular level through computational processing of information derived from living organisms; it underpins every layer of the omics stack.

**Sources**: [[0_Introduzione.01_02_Bioinformatica_e_annotazione_genomi.pdf]]

---

## Definition

Bioinformatics is the scientific discipline that seeks to solve biological problems through the computational processing of information derived — directly or indirectly — from living organisms.

A simpler Wikipedia formulation: *a scientific discipline dedicated to solving biological problems at the molecular level with computational methods.*

## Types of biological information processed

Bioinformatics operates on many data modalities:

| Category | Examples |
|----------|---------|
| Genomic sequences | Whole genomes, exomes, targeted regions |
| Protein sequences | cDNA (mRNA reverse-transcribed to DNA) |
| 3D protein structures | NMR, X-ray crystallography, cryo-EM |
| Medical images | X-ray, CT, MRI, ultrasound |
| Blood/fluid measurements | Particle concentrations |
| Molecular interactions | Systems biology networks |
| Evolutionary information | Phylogenetic data |
| Physiological signals | Heart rate, respiration |

## The omics landscape

Bioinformatics serves as the computational backbone for all "omics" disciplines, which form a cascade from DNA to metabolites:

[[0_Introduzione.01_02_Bioinformatica_e_annotazione_genomi.pdf#page=4|Omics hierarchy — slide 4]]

| Layer               | Studies                                             |
| ------------------- | --------------------------------------------------- |
| **Genomics**        | The genome: structure, content, function, evolution |
| **Transcriptomics** | The full set of RNA transcripts (the transcriptome) |
| **Proteomics**      | The full complement of proteins (the proteome)      |
| **Metabolomics**    | Small molecules and metabolic intermediates         |

Each layer feeds the next: genomic variants affect transcription, transcript levels determine protein abundance, and proteins catalyze the reactions that produce metabolites. Bioinformatics research is oriented toward all four layers simultaneously.

## What genomics studies

[[Genomics]] is the branch of molecular biology concerned with the study of an organism's genome — its structure, content, function, and evolution. Because it generates enormous quantities of data, it depends entirely on bioinformatics for processing and visualisation.

Core genomics tasks:

- **DNA extraction and sequencing** — using cutting-edge technologies such as [[NGS (Next Generation Sequencing)]]
- **Genome assembly** — reconstructing a genome from millions of short DNA fragments
- **Re-sequencing** — mapping new reads to a reference genome
- **Reference alignment** — aligning DNA fragments to a reference
- **Genome annotation** — identifying and characterizing all functional elements in the genome
- **Functional annotation** — assigning biological roles to predicted genes
- **RNA-Seq expression analysis** — measuring gene expression across conditions
- [[Variant calling]] — identifying SNPs and other variants across individuals
- [[GWAS (Genome-Wide Association Studies)]] linking variants to traits

## Why genome annotation matters

With NGS reducing sequencing costs dramatically, the number of sequenced genomes is growing rapidly. The primary goal of sequencing a genome is to understand gene function. While annotation was once expensive and limited to large consortia, modern tools have made it accessible to individual laboratories — though it remains a complex, computationally demanding task.

Annotating a genome means determining the **localization, structure, and function** of every element it contains:

- Protein-coding genes
- Non-coding genes (ncRNA, lncRNA, etc.)
- Regulatory elements (promoters, enhancers)
- Repeated elements (transposons, SINEs, LINEs)
- Pseudogenes
- Other functional elements

For a full treatment of protein-coding gene annotation methods see [[genome-annotation-pipeline]].

## Related pages

- [[genome-annotation-pipeline]]
- [[gene-prediction]]
- [[eukaryotic-gene-structure]]
- [[extrinsic-vs-intrinsic-information]]

## Other sources

- NCBI Bioinformatics resources: overview at ncbi.nlm.nih.gov
- Lesk, *Introduction to Bioinformatics* (Oxford University Press) — textbook overview
- Pevsner, *Bioinformatics and Functional Genomics* — broader omics perspective

## Test yourself

**Q**: What is the definition of bioinformatics?
**A**: The scientific discipline that seeks to solve biological problems through computational processing of information derived from living organisms.

**Q**: Name the four omics layers in hierarchical order.
**A**: Genomics → Transcriptomics → Proteomics → Metabolomics.

**Q**: What are three core tasks of genomics beyond sequencing?
**A**: Genome assembly, genome annotation, and variant calling (also: RNA-Seq analysis, GWAS).
