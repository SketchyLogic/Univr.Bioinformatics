---
tags:
  - __DEFINITION
  - Module1
CreatedAt: 2026-04-29
LastUpdateAt: 2026-04-29
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedBy: claude-sonnet-4-6
---

# Polypyrimidine tract

A stretch of **15–40 pyrimidine nucleotides** (cytosines and thymines) located between the [[Branch point (splicing)]] and the AG acceptor site at the 3′ end of a spliceosomal intron.

**Function**: serves as a binding platform for the splicing factor **U2AF65** (U2 Auxiliary Factor, large subunit). U2AF65 binding to the polypyrimidine tract stabilises the recognition of the branch point by U2 snRNP, promoting spliceosome assembly. A longer, more C/T-rich tract generally means more efficient splicing; a weak tract (interrupted by purines) can cause exon skipping or reduced splicing efficiency.

**Position**:

```
intron ... [branch point A] ── [polypyrimidine tract] ── AG | exon
                ~18–40 bp           ~15–40 bp           acceptor
```

**Relevance to gene prediction**: position weight matrices (PWMs) and WAMs trained on acceptor sites capture the polypyrimidine tract implicitly — the positions immediately upstream of AG show a strong statistical bias toward C and T. This pyrimidine-rich window is one reason acceptor site models extend 20–40 bp into the intron rather than scoring just the AG dinucleotide.

# TLDR

The polypyrimidine tract is a C/T-rich stretch just before the AG acceptor that recruits U2AF65 and promotes spliceosome assembly. Its pyrimidine bias is captured by acceptor site PWMs in gene finders.
