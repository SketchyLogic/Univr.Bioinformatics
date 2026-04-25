---
tags:
  - __CONCEPT
  - Module2
---
# Sequence identity zones

Three empirically defined ranges of pairwise sequence identity (SI) that indicate the reliability of homology inference and structural modeling:

| Zone | SI Range | Interpretation |
|------|----------|----------------|
| **Safe zone** | > 30% | Reliable homology; structures are similar; alignment is trustworthy |
| **Twilight zone** | 10–30% | Uncertain homology; alignment errors common; models unreliable |
| **Midnight zone** | < 10% | Statistically indistinguishable from random; no reliable alignment |

**Practical implications**:
- **Safe zone**: homology modeling produces models with Cα RMSD ~1–2 Å; reliable for drug design and functional inference.
- **Twilight zone**: large modeling errors possible; profile-profile methods (HHpred) are needed to detect homology; homology models should be treated with caution.
- **Midnight zone**: fold recognition methods (threading) are required; sequence-based homology modeling is not applicable.

**Key caveat**: two proteins with <25% SI may still share the same fold (convergent evolution) — structure comparison is more reliable than sequence identity alone.

See [[sequence-alignment]], [[homology-modeling]].
