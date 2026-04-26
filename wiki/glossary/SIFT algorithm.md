---
tags:
  - __CONCEPT
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
# SIFT algorithm

**Sorting Intolerant From Tolerant** — a sequence-based method for predicting whether an amino acid substitution is **damaging** or **tolerated**, based on evolutionary conservation.

**Algorithm**:
1. Query the protein against a database using PSI-BLAST to retrieve homologs.
2. Filter to **orthologs** only (removing paralogs improves accuracy by ~8%).
3. Build a [[Position-Specific Scoring Matrix (PSSM)|PSSM]] from the multiple sequence alignment.
4. At the substituted position, look up the probability p of the **mutant amino acid** in the PSSM.
5. **Decision rule**: if p < **0.05** → predicted **damaging (intolerant)**; p ≥ 0.05 → **tolerated**.

**Core logic**: positions conserved across evolution are functionally important; substitutions at conserved positions are likely deleterious.

**Key limitation**: requires ≥ 10 closely related homologs. Fails when the protein has few known orthologs.

**Notable case**: correctly predicts β-globin **E6V** (sickle cell mutation) as damaging because E6 is evolutionarily conserved — while structure-based methods (PolyPhen) fail because E6V is surface-exposed.

See [[amino-acid-substitutions]], [[Nonsynonymous SNP (nsSNP)]], [[Ortholog]].
