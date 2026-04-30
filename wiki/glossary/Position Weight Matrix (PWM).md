---
tags:
  - __CONCEPT
  - Module1
CreatedAt: 2026-04-25
LastUpdateAt: 2026-04-29
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedBy: claude-sonnet-4-6
---

# Position Weight Matrix (PWM)

A PWM answers one question: **given a short window of sequence, how much does it look like a known signal compared to random DNA?**

## Building the matrix

Start with a set of known, aligned signal sequences — e.g. 1000 confirmed donor splice sites, all aligned so position 1 = the G of GT:

```
pos:    1  2  3  4  5  6  7  8
site1:  G  T  A  A  G  T  C  A
site2:  G  T  G  A  G  T  A  G
site3:  G  T  A  G  G  T  G  A
...
```

Count how often each nucleotide appears at each position across all examples. The result is a frequency matrix:

```
     pos1  pos2  pos3  pos4  ...
A:   0.00  0.00  0.60  0.55
C:   0.00  0.00  0.10  0.10
G:   1.00  0.00  0.20  0.25
T:   0.00  1.00  0.10  0.10
```

Position 1 is always G, position 2 always T — the GT of the donor site. Other positions are less constrained but still biased. This frequency table is the PWM.

## Scoring a new sequence

To ask "is this 8-mer a donor site?", look up the frequency of each observed nucleotide at each position and take the log-ratio against the background[^bg] (e.g. 0.25 per base under a uniform model):

$$\text{score} = \sum_{j=1}^{l} \log_2 \frac{M_{b_j,\, j}}{0.25}$$

- A frequent nucleotide at that position → positive contribution → score rises.
- A rare nucleotide at that position → negative contribution → score falls.
- **Score > 0**: the window looks more like the signal than random DNA.

In practice, a gene finder slides this window across the genome, scores every position, and keeps candidates above a chosen threshold.

## Intuition: a weighted checklist

Each position casts a vote weighted by how strongly that base is preferred there. For a donor site: G at pos 1 is a strong vote ✓, T at pos 2 is a strong vote ✓, weakly preferred bases at other positions cast softer votes. The total score is the sum of all votes.

## Limitation: position independence

The matrix treats each position as voting independently. In reality, adjacent bases are correlated — having G at position 3 may make A at position 4 more likely. A PWM cannot capture this.

This is the motivation for stronger models:
- [[Weight Array Model (WAM)]]: models pairwise dependencies between adjacent positions.
- [[Maximal Dependence Decomposition (MDD)]]: identifies and models the strongest dependencies across all positions.

See [[signal-sensors]] for how PWMs fit into the broader gene prediction pipeline, and [[genscan]] for a practical application.

[^bg]: **Background** is the null model — what random, non-functional DNA looks like at that position. The log-ratio compares the probability of the observed base under the signal model against its probability under background noise. Three common choices, in increasing accuracy: (1) **Uniform** (0.25 each) — simplest, but rarely true; (2) **Genomic frequencies** — uses the actual A/C/G/T proportions of the target genome, correcting for overall GC content; (3) **Local context frequencies** — uses base frequencies in the region surrounding the candidate site, removing local GC bias. Concrete consequence: if position 3 of a donor PWM shows G with frequency 0.20, the uniform background scores it $\log_2(0.20/0.25) = -0.32$; but if that region is GC-rich and G occurs at 0.40 by chance, the correct score is $\log_2(0.20/0.40) = -1.0$. Using the wrong background systematically inflates or deflates scores, which is one reason PWMs trained on one genome do not always transfer cleanly to another.

# TLDR

A PWM is a frequency table of nucleotides at each position of a known signal, used to score new sequences by summing log-likelihood ratios. Fast and interpretable, but assumes positions are independent.
