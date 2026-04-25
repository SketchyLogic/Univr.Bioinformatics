---
tags:
  - __DEFINITION
  - Module1
---
# Position Weight Matrix (PWM)

A matrix that records the **nucleotide (or amino acid) frequency at each position** of a set of aligned functional sequences (e.g., splice sites, promoter elements). Entry w_{i,j} gives the log-odds score of observing nucleotide i at position j relative to its background frequency.

**Score formula**: score = Σⱼ log(f_{i,j} / p_i), where p_i is the background frequency of nucleotide i.

**Key assumption**: **positional independence** — each position contributes independently to the score. This is biologically false (adjacent splice-site positions are correlated) but computationally convenient.

**Limitation**: cannot capture dependencies between positions; treats each column of the alignment as statistically independent.

PWMs are used in [[signal-sensors]] to score splice sites, start codons, and promoter elements. Replaced by [[Weight Array Model (WAM)]] or [[Maximal Dependence Decomposition (MDD)]] when position correlations are strong. See [[genscan]] for practical application.
