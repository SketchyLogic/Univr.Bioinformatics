---
tags:
  - __CONCEPT
  - Module1
CreatedAt: 2026-04-26
LastUpdateAt: 2026-04-26
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedById: claude-sonnet-4-6
---
# Contrast the challenges of gene prediction in prokaryotes and eukaryotes

| Feature                      | Prokaryotes                                                 | Eukaryotes                                                                                         |
| ---------------------------- | ----------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| Gene density                 | ~85–90% coding                                              | ~1.5% coding (human)                                                                               |
| Gene structure               | Uninterrupted ORFs                                          | Exons interrupted by introns; requires splice-site detection (see [[GT-AG rule]], [[Spliceosome]]) |
| Start-site identification    | Aided by [[Shine-Delgarno sequence]] upstream of AUG        | Relies on [[Kozak consensus sequence]]; weaker signal, harder to distinguish from [[Spurious ATG]] |
| Overlapping genes            | Common                                                      | Rare                                                                                               |
| Operons                      | Frequent; multiple genes per transcript                     | Absent (monocistronic mRNAs)                                                                       |
| Alternative splicing         | Absent                                                      | Pervasive; one locus → many protein isoforms (see [[Alternative splicing]])                        |
| Repeat content               | Low                                                         | High (TEs, SINEs, LINEs); masks coding signal                                                      |
| Intron size                  | No introns                                                  | Can reach 100 kb+ — dominant fraction of gene length                                               |
| Main computational challenge | Distinguishing real ORFs from random ones in a dense genome | Correctly delineating exon–intron boundaries across a sparse, repeat-rich genome                   |

**Tools reflect the divide**: prokaryotic finders (GLIMMER, GeneMark) lean on ORF length + codon bias; eukaryotic finders (GENSCAN, AUGUSTUS) need full [[Hidden Markov Model (HMM)|GHMM]] architectures with explicit intron/exon state graphs. See [[gene-prediction-tools]] and [[hidden-markov-models]].
