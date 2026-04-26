---
tags:
  - __DEFINITION
  - Module1
---
# Spurious ATG

An in-frame[^inframe] ATG[^atgaug] codon that is **not** a genuine translation start site. It occurs by chance in a coding or non-coding sequence and is not recognised by the ribosome as an initiation point.

**Why it is a problem**: prokaryotic and eukaryotic genomes contain many ATGs; gene finders must score each candidate start codon to determine whether it is real. A spurious ATG that scores highly can cause a gene prediction to be extended or truncated incorrectly.

**How genuine starts are distinguished from spurious ones**:

| Organism | Discriminating signal |
|----------|-----------------------|
| Prokaryotes | [[Shine-Delgarno sequence]] 5–10 nt upstream; spurious ATGs typically lack it |
| Eukaryotes | [[Kozak consensus sequence]] context around AUG; [[content-sensors]] (codon bias downstream) |

A strong Shine-Dalgarno motif immediately upstream of an ATG is the canonical indicator that the ATG is functional, not spurious — see [[Shine-Delgarno sequence]] for detail.

---

[^atgaug]: The same codon written in two alphabets: in DNA it reads `ATG`, in mRNA (after transcription) thymine becomes uracil and it reads `AUG`. Gene finders scan the DNA → ATG; the ribosome reads the mRNA → AUG. Both refer to the same codon.
[^inframe]: A sequence can be read in three different reading frames (window shifted by 0, 1, or 2 nucleotides). An ATG is "in-frame" when it falls in the same reading frame as the surrounding coding sequence, so codons downstream parse as plausible amino acids rather than quickly hitting a stop codon. Being in-frame is necessary but not sufficient to be a real start site.
