---
tags:
  - __DEFINITION
  - Module1
---
# Weight Array Model (WAM)

An extension of the [[Position Weight Matrix (PWM)]] that captures **1st-order Markov dependencies between adjacent positions**.

**Key difference from PWM**: instead of modelling P(sⱼ) at each position independently, the WAM models the conditional probability P(sⱼ | sⱼ₋₁) — the probability of the nucleotide at position j given the nucleotide at position j−1.

This captures biologically meaningful correlations between adjacent positions in signal sequences. For example, the canonical GT dinucleotide at donor splice sites is not two independent positions — the G and T are correlated.

**Limitation**: captures only first-order (adjacent) dependencies; non-adjacent correlations are still ignored.

Used in [[signal-sensors]] and [[genscan]] for improved splice site scoring over PWMs. Further improved by [[Maximal Dependence Decomposition (MDD)]] for non-adjacent dependencies.
