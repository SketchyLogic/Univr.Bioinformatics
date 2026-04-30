---
tags:
  - __CONCEPT
  - Module1
CreatedAt: 2026-04-30
LastUpdateAt: 2026-04-30
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedBy: claude-sonnet-4-6
---

# Refresher on conditional probabilities

## The definition

The **conditional probability** of event $A$ given that event $B$ has occurred is:

$$P(A \mid B) = \frac{P(A \cap B)}{P(B)}$$

Read it as: *"among all worlds where $B$ is true, what fraction also have $A$?"* It re-weights the probability space so that $B$ is taken for granted.

![[graphics.conditionalProbability.png]]

---

## Applied to bioinformatics: what is $P(\text{window} \mid \text{signal})$?

Suppose you slide a window of length $l$ along a genome and you observe the sequence $w = s_1 s_2 \ldots s_l$ (e.g. `GTAAGC…`). You want to know:

> *If this window really is a signal (say, a splice donor site), how likely is it that it looks exactly like $w$?*

| Symbol                    | Meaning                                                                           |
| ------------------------- | --------------------------------------------------------------------------------- |
| $w = s_1 \ldots s_l$      | the observed nucleotide sequence in the window                                    |
| signal                    | the class "this window is a true functional site"                                 |
| $P(w \mid \text{signal})$ | probability of seeing exactly this sequence, given membership in the signal class |

This probability is estimated by collecting many known signal sequences (positive examples), then measuring how often each base appears at each position.

---

## The joint probability problem

$P(w \mid \text{signal})$ is a **joint** conditional probability over $l$ positions simultaneously:

$$P(s_1, s_2, \ldots, s_l \mid \text{signal})$$

The **probability chain rule** lets you decompose any joint probability exactly, one position at a time:

$$P(s_1, s_2, \ldots, s_l \mid \text{signal}) = P(s_1 \mid \text{signal}) \cdot P(s_2 \mid s_1, \text{signal}) \cdot P(s_3 \mid s_1, s_2, \text{signal}) \cdots$$

Each factor conditions on *all previous bases*. This is exact — no assumption has been made yet. The problem is that it is **intractable**:

- $l = 20$ positions → you need to estimate $4^{20} \approx 10^{12}$ joint frequencies from training data.
- No training set is that large; most combinations are never observed.

---

## The independence assumption: the PWM shortcut

The **positional independence assumption** says:

> Given the class label (signal or background), the base at position $j$ is independent of the bases at all other positions.

Formally: for all $j$,

$$P(s_j \mid s_1, \ldots, s_{j-1}, \text{signal}) = P(s_j \mid \text{signal, position } j)$$

Knowing which bases appeared before position $j$ tells you nothing extra about what will appear at $j$. Under this assumption the chain rule collapses entirely:

$$P(s_1, \ldots, s_l \mid \text{signal}) = \prod_{j=1}^{l} P(s_j \mid \text{signal, position } j)$$

Now you only need $4 \times l$ parameters — one per (base, position) pair — instead of $4^l$. Tractable.

---

## Where $M_{s_j,\, j}$ comes from

The **Position Weight Matrix** (PWM) is the lookup table that stores these per-position conditional probabilities:

$$M_{s_j,\, j} \;=\; P(s_j \mid \text{signal, position } j)$$

It is estimated directly from a curated alignment of known signal sequences: count how often each base $b \in \{A, C, G, T\}$ appears at each column $j$, then divide by the total count at that column.

So the scoring formula:

$$P(\text{window} \mid \text{signal}) = \prod_{j=1}^{l} M_{s_j,\, j}$$

is not a heuristic. It is a **conditional probability**, evaluated under the PWM independence assumption, by a table lookup per position.

---

## Why the independence assumption is acceptable here

The assumption is biologically crude — adjacent bases in a splice site are *not* truly independent — but it is pragmatically effective:

1. **Data efficiency**: real training sets have hundreds to thousands of examples, not billions. The product model is the only one that can be fit reliably.
2. **Interpretability**: each position contributes an independent factor; you can inspect which positions are informative.
3. **Works in practice**: despite its simplicity, PWM scanning finds real splice sites, TF binding sites, and other signals with competitive accuracy.

More expressive models (e.g. Markov chains, neural networks) relax this assumption at the cost of more data and less interpretability.

---

# Connections
See [[Why log2 in PWM scoring]].

# TLDR

$P(\text{window} \mid \text{signal})$ is a joint conditional probability over all positions. The chain rule expands it into an intractable product of context-dependent terms; the **positional independence assumption** collapses it into a simple product of per-position frequencies — which is exactly the PWM scoring formula.
