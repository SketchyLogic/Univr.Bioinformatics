---
tags:
  - __CONCEPT
  - Module1
CreatedAt: 2026-04-27
LastUpdateAt: 2026-04-27
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedBy: claude-sonnet-4-6
---

# Structure of mRNA

A mature eukaryotic mRNA has four regions arranged linearly from 5′ to 3′:

```
5' cap — [ 5' UTR ] — [ CDS ] — [ 3' UTR ] — poly-A tail
                       ATG...stop
```

| Region                    | Description                                                                      | Notes                                                                                                     |
| ------------------------- | -------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **5′ cap**                | Modified guanosine added co-transcriptionally at the 5′ end                      | Protects mRNA from degradation; required for ribosome recruitment; not encoded in the genome              |
| **5′ UTR**                | Untranslated region between the cap and the start codon                          | Contains regulatory elements, including the Kozak sequence that positions the ribosome at the correct ATG |
| **CDS** (coding sequence) | From the start codon (ATG) to and including the stop codon (TAA/TAG/TGA)         | The only region translated into protein                                                                   |
| **3′ UTR**                | Untranslated region between the stop codon and the poly-A tail                   | Contains elements controlling mRNA stability, localization, and the poly-A signal (AATAAA)                |
| **poly-A tail**           | ~200 adenosines added post-transcriptionally after cleavage at the poly-A signal | Not encoded in the genome; added by poly-A polymerase; aids export, stability, and translation            |

## Relevance to gene annotation

The cap defines the **transcription start site (TSS)**; the poly-A cleavage site defines the **3′ end of the transcript**. These are the outermost boundaries of the gene model.

When reverse transcriptase converts a mature mRNA into cDNA, it copies everything between cap and poly-A tail. A **full-length cDNA** therefore captures all four regions, making it possible to read off the complete exon–intron structure of the gene when aligned back to the genome. See [[gold standard for gene annotation]].

Neither the cap nor the poly-A tail is directly encoded: both are added post-transcriptionally, which is why the genomic sequence alone cannot reveal the exact transcript boundaries without experimental evidence.

See also [[eukaryotic-gene-structure]] for the broader genomic context (promoter, introns, splice sites).

# TLDR

Mature mRNA = 5′ cap + 5′ UTR + CDS (ATG → stop) + 3′ UTR + poly-A tail. Only the CDS is translated; only the cap and poly-A tail mark the true transcript boundaries.
