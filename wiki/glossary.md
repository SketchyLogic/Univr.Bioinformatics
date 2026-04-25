# Glossary

**Summary**: Definitions of key terms and concepts from the Univr Bioinformatics course.

**Last updated**: 2026-04-24

---

## A

**Ab initio gene prediction** — Gene prediction using only the target genome sequence, with no extrinsic evidence and no informant genomes. Strictly a subset of de novo prediction.

**AIR (Ambiguous Interaction Restraint)** — In HADDOCK, a distance restraint between active/passive residues of interacting molecules, derived from experimental data (mutagenesis, NMR). Defined as the effective 1/r⁶-averaged distance between all atom pairs.

**AAS (Amino Acid Substitution)** — A change from one amino acid to another at a specific position in a protein, typically caused by an nsSNP.

**Acceptor splice site** — The 3' end of an intron; canonical sequence AG (in RNA). Marks the intron-exon boundary.

**AUGUSTUS** — A GHMM-based eukaryotic gene predictor that supports extrinsic evidence hints and explicitly models short intron length distributions.

---

## B

**Baum-Welch algorithm** — An EM (Expectation-Maximisation) algorithm for learning HMM parameters (transition and emission probabilities) from unlabelled sequence data.

**Branch point** — An intronic adenosine (~20–50 nt upstream of the acceptor site) involved in lariat formation during pre-mRNA splicing.

**BLAST** — Basic Local Alignment Search Tool. Finds High-Scoring Segment Pairs (HSPs) between a query and a database. Fast but not splice-aware; cannot handle introns.

---

## C

**CDS (Coding Sequence)** — The portion of an mRNA (and the corresponding genomic DNA) that encodes the protein, from start codon to stop codon.

**Codon bias** — The non-uniform usage of synonymous codons (those encoding the same amino acid) by an organism; a major source of coding statistics in gene prediction.

**Coarse-grained (CG) model** — A molecular simulation representation where multiple atoms are grouped into a single "bead"; reduces computational cost at the expense of atomic detail. MARTINI is the canonical CG force field for biomolecules.

**Content sensor** — A function that scores a sequence for its likelihood of being coding (exonic) based on statistical properties such as hexamer frequencies and codon bias, as opposed to signal sensors which detect sequence motifs.

**CRF (Conditional Random Field)** — A discriminative probabilistic model that directly models P(states | sequence). Semi-Markov CRFs (SM-CRFs) are the discriminative analogue of GHMMs, used in gene finders like CRAIG and CONTRAST.

---

## D

**De novo gene prediction** — Gene prediction using only the target genome sequence; no external (extrinsic) evidence. Includes ab initio methods as a strict subset.

**Decoding (HMM)** — The problem of finding the most likely hidden state sequence given an observed sequence; solved by the Viterbi algorithm.

**Donor splice site** — The 5' end of an intron; canonical sequence GT (GU in RNA). Marks the exon-intron boundary.

**DOPE (Discrete Optimized Protein Energy)** — A statistical potential for model quality assessment based on atom distance distributions derived from ~1500 crystal structures.

---

## E

**Emission probability** — In an HMM, P(observation | hidden state). In gene finding: the probability of a nucleotide given the genomic region type (exon, intron, etc.).

**EST (Expressed Sequence Tag)** — A short, single-pass cDNA sequence; partial transcript evidence used to guide gene prediction.

**Exon** — A coding segment of a gene that is retained in the mature mRNA after splicing.

**Exon chaining** — A gene prediction approach (e.g., GeneID) where candidate exons are scored independently and then assembled into gene models by dynamic programming.

**Extrinsic information** — In gene prediction, evidence not derived from the target genome sequence: cDNA, ESTs, protein homology.

---

## F

**Force field** — A mathematical description of the interactions between atoms in a molecular simulation. Includes bonded (stretch, bend, torsion) and non-bonded (electrostatic, van der Waals) terms.

**Forward algorithm** — An HMM algorithm that computes the total probability of an observed sequence P(x | model) by summing over all possible hidden state paths.

---

## G

**GENSCAN** — A landmark GHMM-based eukaryotic gene predictor (Burge & Karlin 1997). Uses MDD for donor sites and a 5th-order inhomogeneous Markov model for coding content.

**GHMM (Generalized Hidden Markov Model)** — An HMM extension that explicitly models state duration distributions (not just geometric), allowing more realistic exon/intron length distributions.

**GLIMMER** — A prokaryotic gene finder using Interpolated Markov Models (IMMs); >90% accuracy on bacteria.

**GPHMM (Generalized Pair HMM)** — An HMM that simultaneously aligns and annotates two syntenic genomic sequences; used by SLAM and TWAIN for comparative gene prediction.

**GT-AG rule** — The canonical dinucleotides at donor (GT) and acceptor (AG) splice sites in eukaryotic pre-mRNA. Used as a hard filter in gene prediction; violated by only ~0.1% of human introns (AT-AC U12 introns).

---

## H

**HADDOCK** — A protein-protein/protein-ligand docking software driven by Ambiguous Interaction Restraints (AIRs) derived from experimental data.

**HMM (Hidden Markov Model)** — A probabilistic state machine where the system passes through a sequence of hidden states, each emitting an observable symbol. Defined by: states, alphabet, transition probabilities, emission probabilities, and initial distribution.

**Homology modeling** — Computational prediction of a protein's 3D structure using a homologous protein of known structure (the template).

**HSP (High-Scoring Pair)** — A local alignment found by BLAST between query and database sequence, used as a seed for further extension.

---

## I

**Intron** — A non-coding sequence within a eukaryotic gene that is spliced out of the primary transcript by the spliceosome.

**Intrinsic information** — In gene prediction, information derived solely from the target genome sequence: signal sensors, content sensors, and evolutionary conservation with informant genomes.

---

## L

**Log-likelihood ratio** — In signal detection: log(P(sequence | signal model) / P(sequence | background model)). Scores above zero indicate the sequence is more likely the signal than background.

---

## M

**MARTINI** — A coarse-grained force field where 4 heavy atoms = 1 CG bead. Lennard-Jones potentials reproduce oil/water partition coefficients. Widely used for protein-lipid membrane simulations.

**MDD (Maximal Dependence Decomposition)** — A method for capturing non-adjacent position dependencies in sequence motifs using a decision tree of WAMs; used by GENSCAN for the donor site model.

**MD (Molecular Dynamics)** — Computational simulation of atomic motion by numerically integrating Newton's equations over time; produces a trajectory of positions and velocities.

**MODELLER** — The most widely used homology modeling software. Builds models by satisfying spatial restraints (distances, dihedral angles) derived from template structures, minimising an objective function with MD simulated annealing.

---

## N

**nsSNP (Nonsynonymous SNP)** — A single nucleotide polymorphism in a coding region that causes an amino acid change. Estimated 67,000–200,000 common nsSNPs in humans.

---

## O

**ORF (Open Reading Frame)** — A continuous stretch of codons beginning with a start codon and ending with a stop codon. In prokaryotes, long ORFs are strong indicators of protein-coding genes.

---

## P

**PBC (Periodic Boundary Conditions)** — A technique in MD simulation where the simulation box is replicated infinitely in all directions to avoid surface effects; atoms leaving one face re-enter from the opposite face.

**Phase (intron)** — The position within a codon at which an intron interrupts the coding sequence: phase 0 (between codons), phase 1 (after 1st nt), phase 2 (after 2nd nt). Adjacent exon phases must be compatible.

**Phylo-HMM** — An HMM that models evolution along a phylogenetic tree simultaneously with gene structure along the genome; used by N-SCAN, SHADOWER, CONTRAST.

**PolyPhen** — An AAS prediction method combining sequence conservation, 3D structure features, and Swiss-Prot functional annotation.

**PSSM (Position-Specific Scoring Matrix)** — A matrix where each entry is the log-odds score of observing a specific residue at a specific position in a multiple sequence alignment, relative to background. Used in PSI-BLAST and SIFT.

**PSI-BLAST** — Iterative BLAST that builds a PSSM from search hits and uses it in the next round; detects ~2× more homologs below 40% SI than standard BLAST.

**PWM (Position Weight Matrix)** — A matrix tabulating the frequency of each nucleotide at each position of a set of aligned biological signals (splice sites, promoters). Assumes position independence.

**Purifying selection** — Negative selection removing deleterious mutations from the population; responsible for the conservation of functional sequences and the rarity of damaging nsSNPs.

---

## R

**RMSD (Root Mean Square Deviation)** — A measure of structural similarity between two molecules: the square root of the mean squared distance between equivalent atom positions after optimal superimposition.

---

## S

**SIFT (Sorting Intolerant From Tolerant)** — A sequence-based AAS prediction method using a PSSM from homologous sequences; substitutions with PSSM probability < 0.05 are predicted damaging.

**Signal sensor** — A computational model for detecting short, functionally important sequence motifs (splice sites, start codons, poly-A signals); typically PWMs, WAMs, or Markov chains.

**SM-CRF (Semi-Markov Conditional Random Field)** — A discriminative analogue of a GHMM; directly models P(states | sequence), allowing arbitrary features. Used in CRAIG, CONRAD, CONTRAST.

**Spliceosome** — The ribonucleoprotein complex that removes introns from pre-mRNA. The major (U2-type) spliceosome processes GT-AG introns; the minor (U12-type) processes AT-AC introns.

**SNP (Single Nucleotide Polymorphism)** — A single base variation at a defined position in the genome, present in ≥1% of the population.

---

## T

**Template (homology modeling)** — A protein of known 3D structure used as a reference to build a homology model for a target protein.

**Timestep (MD)** — The discrete time interval Δt used in numerical integration of equations of motion. Typically 1–4 fs for all-atom simulations (limited by bond stretching vibrations).

**Transition probability** — In an HMM, P(next state | current state); governs how the system moves between states.

**Twilight zone** — The sequence identity range (10–30%) where evolutionary relatedness is uncertain and alignment errors are common. Homology models in this zone require careful validation.

---

## V

**Viterbi algorithm** — A dynamic programming algorithm that solves the HMM decoding problem by finding the most likely hidden state sequence given the observed sequence.

---

## W

**WAM (Weight Array Model)** — A 1st-order Markov model for sequence signals, capturing dependencies between adjacent positions. P(S) = P(s₁) × P(s₂|s₁) × … × P(sₙ|sₙ₋₁).
