# Sequence Alignment

**Summary**: Sequence alignment identifies correspondences between biological sequences; methods range from pairwise (BLAST, FASTA) to profile-based (PSI-BLAST, HHpred) and are foundational for homology detection, gene prediction, and protein structure modelling.

**Sources**: [[Notes_Comp_Biology.pdf]] · [[annurev.genom.7.Ng_Henikoff.pdf]]

**Last updated**: 2026-04-24

---

## Why alignment?

Sequence alignment reveals evolutionary relationships and functional similarities between biological sequences. It is the basis for:
- Finding homologous genes and proteins
- Predicting protein structure by [[homology-modeling]]
- Detecting functional conservation for [[amino-acid-substitutions]] prediction
- Mapping expressed sequences (cDNA, ESTs) to the genome for [[gene-prediction]]

## Types of alignment

### Global vs. local

- **Global alignment** (Needleman-Wunsch): aligns the full length of both sequences. Best when sequences are similar across their entire length.
- **Local alignment** (Smith-Waterman): finds the best matching sub-regions. Best for finding conserved domains in otherwise divergent sequences. BLAST uses local alignment.

## The sequence-structure similarity spectrum

(From Eswar et al. 2008, as summarised in Notes_Comp_Biology.pdf)

| Zone | Sequence Identity | Characteristic |
|------|-------------------|----------------|
| Safe zone | > 30% SI | Reliable homology; similar structure inferred |
| Twilight zone | 10–30% SI | Uncertain evolutionary relationship; statistical measure unreliable |
| Midnight zone | < 10% SI | Statistically irrelevant sequence similarity |

At SI > 30%, most protein pairs share similar structure. At SI < 50%, the predicted model begins to diverge significantly from the true structure (Cα RMSD > 1 Å).

## Three classes of alignment methods

### 1. Pairwise sequence alignment

Aligns two sequences. Searches for global or best local alignments.
- **FASTA** (Lipman & Pearson, 1985): heuristic pairwise alignment.
- **BLAST** (Altschul et al., 1990/1997): finds High-Scoring Segment Pairs (HSPs); widely used for database search. Fast but limited to high-similarity pairs.

Limitation: only two sequences at a time; misses distant homologs below ~30% SI.

### 2. Profile-sequence alignment

The query is a **sequence profile** (PSSM or HMM profile) built from a multiple sequence alignment (MSA) of related sequences.

A **PSSM** (Position-Specific Scoring Matrix) captures the conservation and variation at each position:
- High score for amino acids frequently seen at position j
- Low score for rare amino acids at position j

Methods: **PSI-BLAST** (Altschul et al., 1997) — iterative BLAST that builds a PSSM from each round of hits and uses it in the next search. Can detect ~2× more homologs below 40% SI than pairwise BLAST.

HMM profiles (Krogh et al., 1994; Eddy, 1998) represent the family as an HMM; **HMMER** is the standard tool.

### 3. Profile-profile alignment

Both the query and the database are represented as profiles (PSSMs or HMMs). The query profile is compared to profiles of solved structures.

This is the most sensitive approach: detects ~28% more relationships at the superfamily level than profile-sequence methods, and improves alignment accuracy by 15–20%.

The best-known implementation: **HHpred** (Söding, 2005) — pairwise comparison of profile HMMs. HHpred was the top-scoring server in template-based structure prediction at CASP9.

## Multiple Sequence Alignment (MSA)

An MSA aligns *n* sequences simultaneously, revealing conserved positions (functionally important) and variable positions. MSA is the input to:
- PSSM construction (PSI-BLAST, SIFT — see [[amino-acid-substitutions]])
- Profile HMM building (HMMER)
- Phylogenetic analysis
- Conservation-based AAS prediction ([[amino-acid-substitutions|SIFT, PolyPhen]])

MSA errors propagate downstream — a misaligned region will cause errors in the PSSM and any model built from it. MSA quality should always be inspected, especially when SI < 30%.

## Spliced aligners for gene prediction

Standard pairwise aligners cannot handle introns. Spliced aligners extend the model to allow long insertions (= introns) between exon-matching segments:

| Tool | Use case |
|------|---------|
| BLAT | Fast cDNA/EST to genome |
| GMAP | High-accuracy cDNA to genome |
| Exonerate | General; protein or cDNA to genome |
| Genewise | Protein to genome (accounts for frame shifts) |
| BLAST | Rough location only — not splice-aware |

## Related pages

- [[homology-modeling]]
- [[amino-acid-substitutions]]
- [[evolutionary-conservation]]
- [[extrinsic-vs-intrinsic-information]]
- [[gene-prediction-tools]]
- [[sequence-search-tools]]

## Other sources

- Altschul et al. (1997) — BLAST with gapped alignment (PSI-BLAST)
- Söding (2005) — HHpred profile-profile alignment
- Durbin et al. *Biological Sequence Analysis* (1998) — Chapters 2–4

## Test yourself

**Q**: What is the twilight zone in sequence alignment, and why is it problematic?
**A**: The twilight zone (10–30% sequence identity) is the range where it is statistically uncertain whether two sequences are truly homologous. Alignments in this range may be unreliable, making structure predictions based on them error-prone.

**Q**: How does PSI-BLAST differ from BLAST, and why is it more sensitive?
**A**: PSI-BLAST is iterative: after each search, it builds a PSSM from the hits and uses this profile in the next search. Because the profile captures family-level conservation rather than a single query sequence, it detects more distant homologs (roughly twice as many below 40% SI).

**Q**: Why do profile-profile methods outperform profile-sequence methods?
**A**: Because both the query and database are represented as profiles, capturing the sequence variation of both families. This richer representation detects ~28% more superfamily-level relationships and provides more accurate alignments than comparing a profile to a single sequence.
