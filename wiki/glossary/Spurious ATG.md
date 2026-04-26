---
tags:
  - __DEFINITION
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
# Spurious ATG

An in-frame[^1] ATG[^2] codon that is **not** a genuine translation start site. It occurs by chance in a coding or non-coding sequence and is not recognised by the ribosome as an initiation point.

**Why it is a problem**: prokaryotic and eukaryotic genomes contain many ATGs; gene finders must score each candidate start codon to determine whether it is real. A spurious ATG that scores highly can cause a gene prediction to be extended or truncated incorrectly.

**How genuine starts are distinguished from spurious ones**:

| Organism | Discriminating signal |
|----------|-----------------------|
| Prokaryotes | [[Shine-Delgarno sequence]] 5–10 nt upstream; spurious ATGs typically lack it |
| Eukaryotes | [[Kozak consensus sequence]] context around AUG; [[content-sensors]] (codon bias downstream) |

A strong Shine-Dalgarno motif immediately upstream of an ATG is the canonical indicator that the ATG is functional, not spurious — see [[Shine-Delgarno sequence]] for detail.
# TLDR
ATG can be interpreted as start sites, if it is in a coding sequence and in-frame is a Methionine incorporated in the resulting protein

---

[^1]: A sequence can be read in three different reading frames (window shifted by 0, 1, or 2 nucleotides). An ATG is "in-frame" when it falls in the same reading frame as the surrounding coding sequence, so codons downstream parse as plausible amino acids rather than quickly hitting a stop codon. Being in-frame is necessary but not sufficient to be a real start site.
[^2]: The same codon written in two alphabets: in DNA it reads `ATG`, in mRNA (after transcription) thymine becomes uracil and it reads `AUG`. Gene finders scan the DNA → ATG; the ribosome reads the mRNA → AUG. Both refer to the same codon.

