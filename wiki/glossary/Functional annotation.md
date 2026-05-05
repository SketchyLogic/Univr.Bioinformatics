---
tags:
  - __DEFINITION
  - Module1
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

The process of **assigning a biological function to each gene** by characterising the protein it encodes. It is performed after [[Structural gene annotation]] has determined where the genes are and what their exon/intron structure is.

Approaches include:
- **Sequence homology**: BLAST search against a curated protein database (e.g., SWISSPROT, UniProt) to find orthologs with known function
- **Domain/motif search**: HMMER against Pfam, InterPro to identify functional domains
- **GO (Gene Ontology) term assignment**: mapping genes to standardised functional vocabulary (molecular function, biological process, cellular component)
- **Pathway databases**: KEGG, Reactome — placing the gene product in a metabolic or signalling context

Functional annotation is conceptually distinct from structural annotation: the former answers *what does this protein do?*, the latter answers *where is this gene and what are its exons?*

See also: [[gene annotation]], [[Structural gene annotation]], [[Homology]].
