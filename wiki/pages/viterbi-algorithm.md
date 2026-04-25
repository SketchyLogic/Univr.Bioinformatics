# Viterbi Algorithm

**Summary**: The Viterbi algorithm is a dynamic programming method that solves the HMM decoding problem — finding the most likely sequence of hidden states (e.g., exon/intron annotations) given an observed sequence (DNA nucleotides).

**Sources**: [[2.1.gene_prediction_v15.pdf]] · [[Modelli Nascosti di Markov-Gene pred.pdf]]

**Last updated**: 2026-04-24

---

## The decoding problem

Given:
- An HMM with states Q, transition matrix A, emission matrix B, initial distribution π
- An observed sequence x = x₁ x₂ … xₙ (e.g., a DNA sequence)

Find: the state sequence y = y₁ y₂ … yₙ that maximises P(y | x, model).

This is the **decoding problem**, solved by the Viterbi algorithm.

## The core idea

Brute-force enumeration of all possible state paths is intractable (exponential in sequence length). The Viterbi algorithm uses **dynamic programming** to solve it in O(n × |Q|²) time.

**Key insight**: the most likely path to state *i* at position *k* must pass through the most likely path to some state *j* at position *k-1*, followed by the transition j → i.

## Recurrence relation

Define V_k(i) = maximum probability of any state path ending in state i at position k, having emitted x₁…xₖ.

$$V_k(i) = \max_j \left[ V_{k-1}(j) \cdot a_{j \to i} \right] \cdot b_i(x_k)$$

Where:
- $a_{j \to i}$ = transition probability from state j to state i
- $b_i(x_k)$ = emission probability of nucleotide $x_k$ from state $i$

**Initialisation**: $V_1(i) = \pi_i \cdot b_i(x_1)$

**Traceback**: at each position, record which state j achieved the maximum — this builds a backpointer table. After reaching position n, traceback from the highest-scoring state to reconstruct the full path.

## Worked example (from lecture notes)

Observed sequence: A T A T G C G G C

Using the 2-state model (E = Exon, I = Intron):
- P(start → E) = P(start → I) = 0.5

Position 1 (A):
- V₁(E) = 0.5 × P(A|E) = 0.5 × 0.2 = 0.10
- V₁(I) = 0.5 × P(A|I) = 0.5 × 0.4 = 0.20 ← higher

Since P(A|I) > P(A|E), intron is more likely at position 1.

The effect of **transition probabilities**: staying in state I costs ×0.7; switching to E costs ×0.3. This penalises frequent switching — encoding the biological reality that exons and introns are long continuous stretches.

Result: the algorithm assigns I I I I E E E E to the sequence A T A T G C G G C — first 4 AT-rich positions classified as intron, last 5 GC-rich positions as exon.

## Qualitative interpretation

- High self-transition (e.g., P(E→E) = 0.8) → exons tend to be long. This models average exon length.
- High cross-transition would allow nucleotide-by-nucleotide switching — biologically unrealistic.
- The transition probabilities together with length determine the effective length distribution of each state.

## What real gene-finding lacks in this simple model

Real GHMMs extend the 2-state model with:
- Separate states for start codon, stop codon, donor/acceptor sites
- 3-frame exon and intron states (for phase compatibility)
- Higher-order emission models (5th-order Markov for exons, WAMs for splice sites)
- Explicit length distributions (Generalized HMMs, see [[hidden-markov-models]])

But the **mathematical principle is identical**: find the state path that maximises the product of transition and emission probabilities.

## The three HMM algorithms compared

| Problem | Algorithm | Computes |
|---------|-----------|----------|
| Evaluation | Forward | P(x \| model) — sum over all paths |
| Decoding | **Viterbi** | Most likely single path argmax P(y \| x) |
| Learning | Baum-Welch | Parameters that maximise P(x \| model) |

The Forward and Backward algorithms also compute the **posterior probability** P(state i at position k | x, model) for each position — useful when you want soft assignments rather than a single best path.

## In practice

After training an HMM on annotated genomes, the Viterbi algorithm is run on the input genomic sequence. The output is a "parse" — a segmentation of the sequence into labelled states. This parse is the gene structure prediction.

In large-scale genome annotation, the genome is typically split into chunks (separated by long intergenic runs) and each chunk is parsed independently.

## Related pages

- [[hidden-markov-models]]
- [[gene-prediction]]
- [[gene-prediction-tools]]

## Other sources

- Rabiner (1989) — classical HMM tutorial, detailed Viterbi derivation
- Durbin et al. *Biological Sequence Analysis* (1998) — Chapter 3

## Test yourself

**Q**: What does the Viterbi algorithm compute, and why is dynamic programming necessary?
**A**: It finds the single most likely state path (exon/intron segmentation) given the observed sequence. Dynamic programming is necessary because brute-force enumeration of all paths is exponential in sequence length; DP reduces this to polynomial time by reusing sub-path solutions.

**Q**: How do transition probabilities encode biological constraints in a gene-finding HMM?
**A**: High self-transition probabilities (P(E→E), P(I→I)) reflect the fact that exons and introns are long continuous regions. They penalise frequent state switching, so the algorithm only switches states when the emission evidence is strong enough to overcome the transition cost.

**Q**: What is the difference between the Viterbi algorithm and the Forward algorithm?
**A**: Viterbi finds the single **maximum probability** path (argmax). The Forward algorithm sums the probabilities over **all** possible paths to compute the total probability P(x|model). Both use similar DP recurrences but Viterbi uses max while Forward uses sum.

**Q**: In the dishonest casino analogy, what does the Viterbi algorithm do?
**A**: It infers the most likely sequence of which die (fair/loaded = intron/exon) the croupier used at each roll, given only the observed sequence of numbers (= nucleotides).
