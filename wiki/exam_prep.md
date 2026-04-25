# Exam Preparation

**Summary**: Key concepts, flashcards, and structured review sections for all topics in the Univr Bioinformatics wiki. Use this as the primary self-assessment resource.

**Last updated**: 2026-04-24

---

## Section 1 — Gene Prediction

### Core concepts to master

1. The difference between prokaryotic and eukaryotic gene finding difficulty
2. Extrinsic vs. intrinsic information; de novo vs. ab initio
3. Signal sensors: PWMs, WAMs, MDD — what they model and their assumptions
4. Content sensors: codon bias, hexamers, 5th-order Markov model
5. The HMM framework: 5 components, 3 fundamental problems
6. Viterbi algorithm: recurrence, interpretation of transitions
7. GHMM vs. basic HMM: length distribution modelling
8. Phylo-HMMs and comparative gene prediction
9. SM-CRFs: discriminative vs. generative learning
10. Combiner programs: why they outperform individual tools

### Flashcards

**Q**: What is the formal gene prediction problem?
**A**: Given a DNA sequence (chromosome or genome), determine the precise boundaries and exonic structures of all protein-coding genes.

---

**Q**: Why is eukaryotic gene prediction harder than prokaryotic?
**A**: Eukaryotic genomes are orders of magnitude larger (only ~3% coding in humans), genes are split into short exons interrupted by long introns (up to 100+ kb), alternative splicing allows one gene to make multiple transcripts, and genes can be interleaved/overlapping/nested.

---

**Q**: What is the GT-AG rule and why is it important?
**A**: The canonical dinucleotides at donor (5' intron boundary: GT) and acceptor (3' intron boundary: AG) splice sites. Used as a necessary filter in gene prediction — only GT-AG pairs are considered as potential splice site pairs.

---

**Q**: What is a PWM, what does it assume, and what is its limitation?
**A**: A Position Weight Matrix records nucleotide frequencies at each position of aligned functional sequences. It assumes **positional independence** — each position is independent of others. This is biologically false (splice sites have correlated positions) but computationally convenient.

---

**Q**: How does a WAM improve on a PWM?
**A**: A Weight Array Model captures 1st-order Markov dependencies between adjacent positions: P(sⱼ|sⱼ₋₁). This captures that the nucleotide at position j depends on the nucleotide at j-1.

---

**Q**: What is MDD (Maximal Dependence Decomposition)?
**A**: A method that uses a decision tree to select among multiple WAMs based on the most informative positions. Captures non-adjacent position dependencies. Used in GENSCAN for the donor splice site model.

---

**Q**: Why is the 5th-order Markov model for coding sequence 3-periodic (inhomogeneous)?
**A**: Because codon positions 1, 2, and 3 have very different nucleotide compositions (the 3rd position is the "wobble" position, most degenerate). Three separate Markov chains capture the 3-periodic structure of the genetic code.

---

**Q**: What are the 5 components of an HMM?
**A**: (1) Hidden states Q, (2) Observable alphabet Σ, (3) Transition probability matrix A, (4) Emission probability matrix B, (5) Initial state distribution π.

---

**Q**: What are the 3 fundamental HMM problems and their algorithms?
**A**: 
- **Evaluation**: P(sequence | model) → Forward algorithm
- **Decoding**: most likely state path → **Viterbi algorithm**
- **Learning**: estimate parameters → Baum-Welch (EM)

---

**Q**: State the Viterbi recurrence.
**A**: V_k(i) = max_j [V_{k-1}(j) × a_{j→i}] × b_i(x_k)
Where a_{j→i} is the transition probability and b_i(x_k) is the emission probability. Initialise: V_1(i) = π_i × b_i(x_1).

---

**Q**: What is the dishonest casino analogy for gene finding?
**A**: A croupier switches secretly between a fair die (= intron, AT-rich) and a loaded die (= exon, GC-rich). We observe numbers (= nucleotides) but not which die (= functional state). Viterbi finds the most likely sequence of dice = most likely exon/intron annotation.

---

**Q**: What limitation of basic HMMs do Generalized HMMs (GHMMs) address?
**A**: Basic HMMs model state duration as a geometric distribution. Real exon/intron lengths follow non-geometric distributions. GHMMs explicitly model duration distributions (e.g., Poisson) by drawing a duration d on state entry and emitting d symbols.

---

**Q**: What is the key advantage of a Phylo-HMM over a GHMM?
**A**: A Phylo-HMM models the evolutionary history of the DNA sequence along a phylogenetic tree simultaneously with gene structure. Coding and non-coding regions have different evolutionary rates, providing an additional orthogonal signal for gene prediction.

---

**Q**: What makes SM-CRFs discriminative (vs. HMMs which are generative)?
**A**: HMMs model the joint P(x, y) of observations and states, then compute P(y|x) via Bayes rule. SM-CRFs directly model P(y|x), allowing: (1) arbitrary overlapping features, (2) no need for a probabilistic model of the input, (3) parameters optimised to directly maximise annotation accuracy.

---

**Q**: Why do combiner programs outperform individual gene predictors?
**A**: They combine predictions from multiple tools that make partially uncorrelated errors. The signal-to-noise ratio increases when errors cancel each other out. Combiners typically improve specificity substantially.

---

### Linear review: gene prediction

1. **The problem** → [[gene-prediction]]
2. **Gene anatomy** → [[eukaryotic-gene-structure]]
3. **Two types of evidence** → [[extrinsic-vs-intrinsic-information]]
4. **Signal models** → [[signal-sensors]] (PWM → WAM → MDD → SVM)
5. **Content models** → [[content-sensors]] (hexamers, 5th-order Markov)
6. **Integration framework** → [[hidden-markov-models]] (GHMM, Phylo-HMM, SM-CRF)
7. **Decoding** → [[viterbi-algorithm]]
8. **Tools** → [[gene-prediction-tools]]
9. **Conservation signal** → [[evolutionary-conservation]]

---

## Section 2 — Protein Structure & Computational Methods

### Core concepts to master

1. Sequence identity zones: safe, twilight, midnight
2. Steps in homology modeling: search → align → build → refine → assess
3. Five error categories in homology models
4. MODELLER: spatial restraints, objective function, SA minimisation
5. Docking components: scoring function + search method
6. HADDOCK: AIRs, 3-step protocol, scoring equation
7. Autodock vs. Vina: scoring functions, search strategies
8. MD basics: force field, timestep, integration, PBC
9. Solvation: explicit vs. implicit solvent
10. Coarse-grained MD: MARTINI, mapping strategy

### Flashcards

**Q**: What are the three sequence identity zones and their ranges?
**A**: 
- **Safe zone**: >30% SI — reliable homology, similar structure
- **Twilight zone**: 10–30% SI — uncertain homology, unreliable alignment
- **Midnight zone**: <10% SI — statistically irrelevant

---

**Q**: What are the five steps of homology modeling?
**A**: (1) Template search & target-template alignment, (2) Template selection, (3) Initial model construction, (4) Model refinement, (5) Model quality assessment.

---

**Q**: What are the five categories of errors in homology models?
**A**: (1) Side-chain errors, (2) Structural deviations in correctly aligned regions, (3) Errors from incorrect alignment, (4) Distortions in misaligned/indel regions, (5) Errors from incorrect/fragmentary templates.

---

**Q**: How does MODELLER build a homology model?
**A**: Extracts spatial restraints (interatomic distances, backbone angles φ/ψ) from template(s), associates each with a probability density function, combines them with CHARMM force field constraints into an objective function, then minimises violations using variable target function method + MD with simulated annealing.

---

**Q**: What is an AIR in HADDOCK?
**A**: An Ambiguous Interaction Restraint: an ambiguous distance restraint between active/passive residues of two interacting molecules, derived from experimental data. Defined as d_eff = (Σ 1/r⁶)^(-1/6), ensuring it is satisfied when any atom pair comes into contact.

---

**Q**: What are the three steps of the HADDOCK docking protocol?
**A**: (1) Rigid body energy minimisation (EM), (2) Semi-rigid simulated annealing in torsion angle space (TAD-SA), (3) Final refinement in Cartesian space with explicit solvent.

---

**Q**: What is the HADDOCK final score formula?
**A**: FS = 1×Elec + 1×vdW + 1×Dsolv + 1×AIR (electrostatics, van der Waals, desolvation, AIR energy)

---

**Q**: What is the main difference between Autodock and Vina?
**A**: Autodock uses an empirical free-energy force field + Lamarckian genetic algorithm; includes explicit electrostatics and H-bond terms. Vina uses a simpler gradient-optimised scoring function without explicit electrostatics; faster but less physically detailed.

---

**Q**: Why is the timestep in MD simulations restricted to 1–4 fs?
**A**: Because the fastest motions in the system are bond stretching/bending vibrations with periods ~10 fs. The timestep must be small enough to accurately integrate these fast motions; larger timesteps produce artefacts or numerical instability.

---

**Q**: What is the ergodic hypothesis in MD?
**A**: Given infinite time, a system will pass through all possible states. Therefore, time averages from a long MD simulation equal ensemble averages. In practice, convergence is assessed when observables stop changing with time.

---

**Q**: What is the MARTINI coarse-grained force field mapping strategy?
**A**: 4 heavy atoms (MM) → 1 CG bead. Non-bonded Lennard-Jones parameters reproduce oil/water partition coefficients. Bonded parameters from statistical polypeptide data (PDB). Electrostatics treated explicitly. Widely used for protein-lipid membrane simulations.

---

**Q**: What is the difference between explicit and implicit solvent?
**A**: Explicit: individual water molecules are simulated — more accurate, captures hydration shell and dynamics, but computationally expensive. Implicit: solvent modelled as a continuum dielectric — faster, but less accurate (misses water-mediated interactions, entropic effects).

---

## Section 3 — Amino Acid Substitutions and Protein Function

### Core concepts to master

1. Definition and scale of nsSNPs
2. Two biological observations underpinning AAS prediction
3. SIFT: algorithm, threshold, limitation
4. PolyPhen: what it adds over sequence-only methods
5. Coverage trade-off: structure (14%) vs. sequence (81%)
6. β-globin E6V: why structure-based methods fail
7. Mendelian vs. complex disease applications
8. nsSNP frequency and purifying selection evidence
9. Orthologs vs. paralogs in MSA for SIFT

### Flashcards

**Q**: What are the two biological observations underlying AAS prediction?
**A**: (1) Mutations affecting function tend to occur at **evolutionarily conserved** positions. (2) Mutations affecting function tend to occur at **buried** (not solvent-accessible) positions in protein structure.

---

**Q**: How does SIFT predict whether a substitution is damaging?
**A**: SIFT aligns the protein to homologs, builds a PSSM, and looks up the probability of the new amino acid at the substituted position. If probability < 0.05 → predicted **damaging (intolerant)**; ≥ 0.05 → **tolerated**.

---

**Q**: Why does SIFT predict β-globin E6V as damaging (correctly) while PolyPhen predicts it as tolerated?
**A**: E6V is a surface-exposed substitution. Structure-based methods (PolyPhen's structural component) predict surface residues as neutral because they assume surface positions are structurally unimportant. SIFT correctly classifies it as damaging because the E6 position is **evolutionarily conserved** in β-globin orthologs.

---

**Q**: What is the coverage limitation of structure-based AAS methods?
**A**: Only ~14% of nsSNPs have available protein structures. Structure-based methods can only predict AAS effects for proteins with a solved crystal structure or a reliable homology model (>40% SI). Sequence-based methods achieve up to 81% coverage.

---

**Q**: What is the evidence that damaging nsSNPs are under purifying selection?
**A**: (1) nsSNPs predicted damaging by AAS methods have lower minor allele frequencies than neutral ones. (2) Non-conservative changes (e.g., hydrophobic → charged) survive at half the rate of conservative changes. (3) nsSNPs overall comprise only half of observed coding SNPs (the rest are synonymous, which don't change amino acids).

---

**Q**: Why do AAS prediction methods use orthologs rather than paralogs in their MSAs?
**A**: Paralogs are related genes that may have diverged in function. Positions important in one paralog may vary in another without functional consequence. Using orthologs (same gene in different species) ensures the alignment reflects positions conserved for the same function, improving prediction accuracy by ~8%.

---

**Q**: What percentage of disease database AASs (OMIM, HGMD) are predicted damaging by AAS methods?
**A**: 70–90%, compared to only 10–20% of neutral AASs. This high discriminatory power makes AAS methods useful for identifying causative mutations.

---

## Section 4 — Sequence Alignment

### Flashcards

**Q**: What is the twilight zone and why is it problematic?
**A**: Sequence identity range 10–30% where evolutionary relatedness is uncertain. Alignments are unreliable; homology models and structure predictions built from them may have serious errors.

**Q**: How does PSI-BLAST differ from BLAST and why is it more sensitive?
**A**: PSI-BLAST is iterative: it builds a PSSM from hits after each round and uses this profile in the next search. The profile captures family-level variation rather than a single sequence, detecting ~2× more distant homologs below 40% SI.

**Q**: Why are profile-profile methods (HHpred) more sensitive than profile-sequence methods (PSI-BLAST)?
**A**: Both query and database are represented as profiles, capturing the sequence variation of both families. Detects ~28% more superfamily-level relationships; alignment accuracy improves by 15–20%.
