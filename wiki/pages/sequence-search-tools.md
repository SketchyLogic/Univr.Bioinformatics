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
# Sequence Search Tools

**Summary**: A reference for the major sequence database search tools — BLAST, PSI-BLAST, HMMER, HHpred, BLAT, and GMAP — covering search strategy, sensitivity, and appropriate use cases.

**Sources**: [[Notes_Comp_Biology.pdf]] · [[2.1.gene_prediction_v15.pdf]]

**Last updated**: 2026-04-25

---

## Overview

Sequence database search is the first step in most comparative genomics and structural biology workflows: finding homologs, identifying template structures for [[homology-modeling]], locating expressed sequences in the genome for [[gene-prediction]], and detecting conserved positions for [[amino-acid-substitutions]] prediction.

Tools differ primarily in **sensitivity** (ability to detect distant homologs) and **speed**, driven by whether they compare single sequences, profiles, or profile-to-profile.

| Tool | Method | Sensitivity | Speed |
|------|--------|------------|-------|
| BLAST | Pairwise sequence | Low (>30% SI reliable) | Very fast |
| PSI-BLAST | Profile-sequence (iterative) | Medium (~2× BLAST below 40% SI) | Fast |
| HMMER | Profile HMM–sequence | Medium-high | Moderate |
| HHpred | Profile-profile | Highest (~28% more superfamily hits) | Slow |
| BLAT | Spliced alignment cDNA→genome | N/A | Very fast |
| GMAP | Spliced alignment cDNA→genome | N/A (high accuracy) | Moderate |

For the broader alignment context see [[sequence-alignment]].

## BLAST (Basic Local Alignment Search Tool)

Altschul et al., 1990 / 1997.

**Strategy**:
1. Index the database by short words (k-mers).
2. Find exact or near-exact k-mer matches (seeds / **High-Scoring Segment Pairs, HSPs**).
3. Extend seeds without gaps until score drops below threshold.
4. Extend with gaps to produce final alignments.
5. Report hits below an E-value threshold (default 10).

**Variants**:

| Program | Query | Database |
|---------|-------|---------|
| blastn | nucleotide | nucleotide |
| blastp | protein | protein |
| blastx | translated nucleotide | protein |
| tblastn | protein | translated nucleotide |

**Limitations**:
- Reliable only above ~30% sequence identity.
- Not splice-aware — cannot align cDNA to genomic sequence with introns.
- Used as a rough location step in gene prediction before spliced aligners (BLAT, GMAP).

## PSI-BLAST (Position-Specific Iterated BLAST)

Altschul et al., 1997.

**Strategy**:
1. Run a standard BLAST search with the query sequence.
2. Build a **PSSM** (Position-Specific Scoring Matrix) from aligned hits above a threshold.
3. Use the PSSM as the new query for the next iteration.
4. Repeat until convergence (no new hits added).

A PSSM captures family-wide conservation: conserved positions score high only for the consensus amino acid; variable positions tolerate more substitutions.

**Sensitivity**: detects approximately **twice as many homologs** below 40% SI compared to single-sequence BLAST.

**Caution**: PSI-BLAST can drift if distant false-positive hits enter the PSSM — the profile shifts away from the true family. Threshold selection and manual curation of included sequences matter, especially in the twilight zone.

## HMMER

Krogh et al., 1994; Eddy, 1998.

Builds a **profile HMM** from a multiple sequence alignment (MSA). Profile HMMs explicitly model insertions and deletions per position (match, insert, delete states) and capture position-specific substitution frequencies more accurately than PSSMs.

Standard tool underlying protein family databases (Pfam, PANTHER).

- **`hmmbuild`**: constructs a profile HMM from a MSA.
- **`hmmsearch`** / **`hmmscan`**: searches a sequence against profile HMM databases.

HMMER provides better-calibrated E-values than BLAST and is more sensitive for divergent family members.

## HHpred (Profile-Profile Alignment)

Söding, 2005.

The most sensitive approach: both query and database are represented as **profile HMMs**; the comparison is profile-to-profile.

**Why more sensitive**: a profile encodes the evolutionary variation of a family, not just one representative. Comparing two profiles captures the compatible diversity of both families simultaneously.

**Performance**: detects approximately **28% more superfamily-level relationships** than profile-sequence methods, and improves alignment accuracy by 15–20%.

HHpred was the top-scoring server in template-based structure prediction at CASP9. It is the recommended tool for template search in [[homology-modeling]] when PSI-BLAST fails to find templates (twilight zone, <30% SI).

**Practical workflow**:
1. Build a profile HMM of the query using PSI-BLAST or HMMER against a large sequence database.
2. Compare the profile against a database of profiles built from proteins of known structure (PDB70).
3. Select the best-scoring template and use the HHpred alignment as input to MODELLER.

## BLAT (BLAST-Like Alignment Tool)

Kent, 2002.

**Splice-aware aligner** for mapping cDNA/mRNA/EST sequences to a genome:
- Pre-indexes the genome (not the query) — much faster than BLAST for DNA-to-DNA alignment.
- Models long gaps (introns) explicitly.
- Used to provide extrinsic evidence to gene finders (see [[extrinsic-vs-intrinsic-information]]).
- Available interactively on the UCSC Genome Browser.

**Limitation**: fast but less accurate than GMAP for divergent sequences.

## GMAP (Genomic Mapping and Alignment Program)

Wu & Watanabe, 2005.

High-accuracy cDNA/EST-to-genome aligner. Compared to BLAT:
- Handles more divergent cDNA sequences.
- Better at resolving ambiguous splice sites.
- Slower but preferred for high-quality genome annotation pipelines.

Both BLAT and GMAP feed spliced-alignment evidence into genome annotation pipelines (see [[gene-prediction-tools]]).

## Choosing the right tool

| Use case | Recommended tool |
|----------|-----------------|
| Rapid similarity search, SI > 30% | BLAST |
| Finding distant homologs (sequence-based) | PSI-BLAST or HMMER |
| Template search for homology modeling | HHpred (after PSI-BLAST fails) |
| Family / domain annotation | HMMER against Pfam |
| Mapping cDNA to genome (fast, interactive) | BLAT |
| Mapping cDNA to genome (high accuracy) | GMAP |

## Related pages

- [[sequence-alignment]]
- [[homology-modeling]]
- [[gene-prediction-tools]]
- [[extrinsic-vs-intrinsic-information]]
- [[evolutionary-conservation]]

## Other sources

- Altschul et al. (1990) — original BLAST paper. *J. Mol. Biol.* 215:403–410
- Altschul et al. (1997) — gapped BLAST and PSI-BLAST. *Nucleic Acids Res.* 25:3389–3402
- Söding J. (2005) — HHpred profile-profile alignment. *Bioinformatics* 21:951–960
- Eddy SR. (1998) — Profile hidden Markov models. *Bioinformatics* 14:755–763
- Kent WJ. (2002) — BLAT. *Genome Research* 12:656–664
- Wu TD. & Watanabe CK. (2005) — GMAP. *Bioinformatics* 21:1859–1875

## Test yourself

**Q**: What is the core difference between BLAST and PSI-BLAST in terms of query representation?
**A**: BLAST uses the query sequence directly. PSI-BLAST iteratively builds a PSSM from the homologs found in each round, so the query becomes a position-specific profile of the entire family rather than a single sequence. This detects approximately twice as many distant homologs below 40% SI.

**Q**: Why is HHpred more sensitive than PSI-BLAST?
**A**: HHpred compares profile HMMs to profile HMMs — both query and database are represented as profiles. PSI-BLAST compares a profile to individual sequences. The profile-to-profile comparison captures the compatible evolutionary variation of both families, detecting ~28% more superfamily-level relationships.

**Q**: Why can't standard BLAST be used to map cDNA to a genomic locus?
**A**: Genomic sequence contains introns — long regions absent from the cDNA. A standard local aligner treats these as mismatches or gaps with a standard gap penalty, effectively breaking the alignment. Spliced aligners (BLAT, GMAP) explicitly model long intron-sized gaps.

**Q**: When should you prefer GMAP over BLAT?
**A**: When accuracy matters more than speed — for high-quality genome annotation, divergent cDNA sequences, or when BLAT produces ambiguous splice-site assignments. BLAT is preferred for interactive genome browsing and large-scale rapid surveys.
