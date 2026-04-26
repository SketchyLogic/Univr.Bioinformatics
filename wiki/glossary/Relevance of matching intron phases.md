---
tags:
  - __CONCEPT
  - Module1
---
# Relevance of matching intron phases

## What it is

Every intron interrupts the coding sequence at a specific position within a codon — its **phase** (0, 1, or 2). The exon upstream of an intron has a **donor phase**; the exon downstream has an **acceptor phase**. For the protein reading frame to be preserved after splicing, these two phases must match: the codon split open by the donor site must be completed by the same acceptor site.

See [[Intron phase]] for the three cases.

## Why it matters biologically

If the donor and acceptor phases do not match, the joined sequence is read in the wrong frame downstream of the junction — a **frameshift**. This almost always produces a premature stop codon, rendering the resulting protein non-functional or absent (nonsense-mediated decay). Phase mismatch is therefore strongly lethal at the molecular level and is almost never observed in real, functional splice junctions.

## Why it is a useful constraint for gene prediction

Gene finders like [[genscan|GENSCAN]] and [[hidden-markov-models|GHMM]]-based tools model intron phases as **separate HMM states**: `intron-phase-0`, `intron-phase-1`, `intron-phase-2`. The transition probabilities between states enforce phase compatibility — a donor-phase-1 state can only connect to an acceptor-phase-1 state.

This constraint:
- **Prunes the search space**: the model never considers splice-junction combinations that would produce a frameshift, eliminating a large class of false positives.
- **Adds discriminative power**: two candidate splice sites that look equally good by signal alone (PWM score, GT-AG dinucleotides) are distinguished by whether their phases are compatible in the context of the surrounding exon chain.
- **Improves exon chaining**: when assembling multi-exon gene models, phase compatibility forces a globally consistent reading frame across all junctions simultaneously.

## When non-matching phases can still yield a predicted gene

There are a few situations where a phase mismatch does not prevent a locus from being predicted as a gene:

1. **Compensatory frameshifts**: two introns with mismatched phases that together cancel out (e.g., +1 then −1) restore the reading frame. The individual junctions are "wrong" in isolation but correct in combination. Rare but observed in some lineage-specific genes.

2. **Alternative splicing isoforms**: one isoform uses a phase-compatible junction; another isoform skips that exon entirely (exon skipping). A gene finder that models only a single transcript may still call the locus as a gene using the canonical isoform, even if other splicing patterns would produce mismatches.

3. **Annotation / training error**: if the gene finder was trained on a dataset containing mis-annotated phase combinations, it may assign non-zero transition probabilities to incompatible phase pairs and occasionally predict them.

4. **Non-canonical splice sites**: the ~1% of introns with AT-AC boundaries (processed by the minor spliceosome) follow different consensus rules. A tool trained only on GT-AG introns may mismodel their phases.

## Related

[[Intron phase]] · [[eukaryotic-gene-structure]] · [[hidden-markov-models]] · [[genscan]] · [[Alternative splicing]] · [[Spliceosome]]
