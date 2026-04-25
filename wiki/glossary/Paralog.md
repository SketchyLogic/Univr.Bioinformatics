---
tags:
  - __DEFINITION
  - Module3
---
# Paralog

A gene related to another gene by **gene duplication** (within the same or different genome), rather than by speciation. Paralogs can diverge in sequence, structure, and function.

**Contrast with [[Ortholog]]**: orthologs are related by speciation and typically retain the same function.

**Why paralogs are problematic for AAS prediction**: in an MSA that includes paralogs, a position that is functionally essential in the query protein may be freely variable in a paralog that has diverged to a different function. This inflates the apparent tolerance for substitutions at important positions, reducing [[SIFT algorithm|SIFT]] prediction accuracy.

**Example**: the human hemoglobin subunits α, β, γ, and δ are paralogs — products of ancient gene duplications. They share a structural fold but have different O₂ binding affinities and expression profiles. Including all four when building an MSA to assess β-globin variants would add misleading variation at functionally critical positions.

**Solution**: filter MSAs to orthologs or use species-specific databases to ensure the alignment reflects conservation of the same function.

See [[amino-acid-substitutions]], [[Ortholog]].
