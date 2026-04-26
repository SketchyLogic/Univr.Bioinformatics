---
tags:
  - __DEFINITION
  - Module1
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
# Kozak consensus sequence

The nucleotide context surrounding the **AUG start codon** in eukaryotic mRNA that promotes efficient ribosome recognition and translation initiation.

**Consensus**: `(gcc)gccRccAUGG`  
Key positions: a purine (**R** = A or G) at position −3, and **G** at position +4 (immediately after AUG), are the most critical for translation efficiency.

**Role in gene prediction**: used as a [[signal-sensors|signal sensor]] to distinguish genuine translation start sites from spurious in-frame ATGs in eukaryotic gene finders (e.g., [[genscan|GENSCAN]], [[gene-prediction-tools|AUGUSTUS]]).

**Contrast with prokaryotes**: prokaryotic ribosomes use the [[Shine-Delgarno sequence]] for ribosome positioning. Eukaryotes instead use cap-dependent scanning — the ribosome binds the 5′ cap and scans for the first AUG in a favorable Kozak context.

See [[eukaryotic-gene-structure]], [[signal-sensors]].
