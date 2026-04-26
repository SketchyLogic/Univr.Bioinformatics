---
tags:
  - __EXECUTABLE
  - Module3
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
# Predict whether an nsSNP is damaging using SIFT

**Given**: a protein sequence and a single amino acid substitution at position p (e.g., E6V in β-globin: glutamate → valine at position 6).

**Step-by-step**:

1. **Run PSI-BLAST** from the query protein to retrieve homologs from a protein database (e.g., UniRef90).
2. **Filter to orthologs** — remove paralogs and sequences that are too divergent or too similar.
3. **Build a [[Position-Specific Scoring Matrix (PSSM)|PSSM]]** from the multiple sequence alignment of orthologs.
4. **Look up the PSSM score** for the mutant amino acid (V in E6V) at position p.
5. **Apply threshold**: if normalised probability < **0.05** → predict **damaging (intolerant)**; p ≥ 0.05 → **tolerated**.

**Interpretation logic**: a low probability means the mutant residue has never been observed at that position during evolution → position is under purifying selection → substitution likely disrupts function.

**Common pitfalls**:
- Too few homologs (<10) → insufficient statistical power → unreliable prediction.
- Including paralogs instead of orthologs → inflates apparent tolerance → false negatives.

**Exam case**: β-globin E6V → SIFT predicts **damaging** (E6 is conserved), PolyPhen predicts **tolerated** (surface-exposed). SIFT is correct because the position is evolutionarily conserved despite being surface-exposed.

See [[SIFT algorithm]], [[amino-acid-substitutions]], [[Ortholog]].
