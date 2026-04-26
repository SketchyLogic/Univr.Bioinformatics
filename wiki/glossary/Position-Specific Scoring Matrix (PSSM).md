---
tags:
  - __DEFINITION
  - Module2
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
# Position-Specific Scoring Matrix (PSSM)

A matrix of log-odds scores where each **column** corresponds to a position in an aligned protein (or nucleotide) sequence and each **row** to an amino acid (or nucleotide). Entry PSSM[j][a] gives the log-odds score of observing residue a at position j, relative to background frequency.

**Construction**:
1. Collect a multiple sequence alignment (MSA) of homologs.
2. Count residue frequencies at each position.
3. Apply pseudocounts to handle sparse positions (avoid log(0)).
4. Normalise and convert to log-odds: log(f_{j,a} / p_a)

**Use in PSI-BLAST**: after an initial BLAST search, PSI-BLAST builds a PSSM from hit sequences and uses it in the next search iteration. The profile captures family-level variation, detecting ~2× more distant homologs than a single-sequence query (below 40% SI).

**Use in SIFT**: at the substituted position, SIFT looks up the PSSM probability of the mutant amino acid to assess whether the position is evolutionarily conserved.

See [[sequence-search-tools]], [[amino-acid-substitutions]], [[SIFT algorithm]].
