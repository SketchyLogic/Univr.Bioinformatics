---
tags:
  - __DEFINITION
  - Module1
---
# Forward algorithm

A **dynamic programming** algorithm that solves the evaluation problem for [[Hidden Markov Model (HMM)|HMMs]]: computing the total probability P(observation sequence | model) by summing over **all** possible state paths.

**Recurrence**:

```
α_k(i) = [ Σ_j α_{k-1}(j) × a_{j→i} ] × b_i(x_k)
```

where α_k(i) = P(x₁…xₖ, state i at position k). Initialisation: α₁(i) = πᵢ × bᵢ(x₁).

**Result**: P(x | model) = Σᵢ αT(i)

**Contrast with Viterbi**: the Forward algorithm **sums** over all paths (total probability); Viterbi takes the **max** (single best path). The Forward algorithm is used in:
- The [[Baum-Welch algorithm]] E-step (with the Backward algorithm)
- Model comparison (which of two HMMs better explains the sequence)
- Posterior decoding (probability of being in a state at each position)

See [[hidden-markov-models]], [[Viterbi algorithm]].
