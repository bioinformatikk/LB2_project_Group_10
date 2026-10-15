# 04 - Feature choices and literature

## Scope

We extended the course's 20 composition features and two hydropathy summaries with nine sequence-only descriptors, giving 31 features in [notebook section 2](../notebooks/04_svm_method.ipynb). The group executed the complete extractor on 8,146 training proteins and obtained 31 columns with no missing values. Classifier evaluation by CV remains pending.

The hydropathy descriptors reuse the Kyte–Doolittle (KD) profile over the first 40 residues, with complete windows of 5 positions. We listed the slide-proposed categories first (charge and the two propensity scales), followed by our four additional sequence descriptors. All specific implementations were documented with their sources. The definitions below follow their order in the extractor.

Both scale profiles preserve unknown positions and average known residues inside each original window, following the policy in notebook section 1.2. Missing windows are omitted from the summaries. An empty or entirely missing profile gives NaN for both summaries. All means are over window values, rather than raw residue values.

## Features

### 1. N-terminal charge balance

**Definition:** `nterminal_charge` calculates `(K + R - D - E counts) / canonical residue count` in the first 5 positions. H and other canonical residues score zero; unknown residues are excluded from the denominator. No canonical residues gives NaN.

**Rationale:** [Guo et al. (2018), *Positive charge in the n-region of the signal peptide contributes to efficient post-translational translocation of small secretory preproteins*](https://pubmed.ncbi.nlm.nih.gov/29229776/) provide experimental evidence for a role of n-region charge in that pathway.

**Limitations:** the first-5 region and treatment of H are simplifying project choices. This dimensionless proxy does not estimate physical net charge at a given pH, and the study does not validate our formula or its value for SP classification.

### 2. Alpha-helix propensity: mean and maximum

**Definition:** `alpha_helix_features` returns `alpha_helix_profile_mean_w5` and `alpha_helix_max_w5`. We map the first 40 residues to the Chou–Fasman alpha-helix scale, build complete 5-position window means, then take the mean and maximum of that profile. The scale values are stored with the common definitions in notebook section 1.2.

**Rationale:** [Chou and Fasman (1978)](https://pubmed.ncbi.nlm.nih.gov/364941/) describe secondary-structure prediction from sequence. Their alpha-helix propensity values, available in [ProtScale](https://web.expasy.org/protscale/pscale/alpha-helixFasman.html), summarize amino-acid frequencies in known structures. Slides 31 and 34 propose secondary-structure scales and the same profile-based approach used for hydropathy.

**Limitations:** we use the published residue scale, not the complete Chou–Fasman prediction algorithm. The profile summaries do not assign secondary structure to individual residues. The first-40 region and window of 5 are fixed project choices, and their value for SP classification remains to be evaluated.

### 3. Transmembrane tendency: mean and maximum

**Definition:** `tm_tendency_features` returns `tm_tendency_profile_mean_w19` and `tm_tendency_max_w19`. We map the first 40 residues to the Zhao–London transmembrane-tendency scale, build complete 19-position window means, then take their mean and maximum. Higher scale values indicate greater transmembrane tendency.

**Rationale:** [Zhao and London (2006), *An amino acid “transmembrane tendency” scale that approaches the theoretical limit to accuracy for prediction of transmembrane helices: Relationship to biological hydrophobicity*](https://doi.org/10.1110/ps.062286306) derived a residue scale by comparing transmembrane and soluble sequences. The values, stored in notebook section 1.2, are available in [ProtScale](https://web.expasy.org/protscale/pscale/Transmembranetendency.html). This directly addresses the transmembrane-propensity category on slide 31.

**Limitations:** the first-40 region and window of 19 are our choices for summarizing a broader segment, not optimized settings or a reproduction of the paper's full analysis. These indices are not TM probabilities or topology predictions. Correlation with hydropathy is expected; any added predictive value must be evaluated within CV.

### 4. Hydropathy peak position

**Definition:** `hydropathy_peak_position` returns the 1-based center of the first maximum window in the KD profile. Missing windows retain their positions; an empty or entirely missing profile gives NaN.

**Rationale:** [Imai et al. (2011), *Eukaryote-wide sequence analysis of mitochondrial β-barrel outer membrane proteins*](https://link.springer.com/article/10.1186/1471-2164-12-79) align SP-related regions around a hydropathy peak to calculate regional descriptors.

**Limitations:** their classifier targets mitochondrial outer-membrane proteins and uses different smoothing and peak-selection rules. Our use of peak position as an SVM input is an adaptation, not their published feature set. The position is not a cleavage-site prediction.

### 5. Hydrophobic stretch extent

**Definition:** `hydrophobic_stretch_length` measures the residue span of the longest contiguous run of KD windows with mean greater than 0. A run of r overlapping windows covers r + 5 − 1 residue positions. No qualifying window gives 0; missing windows break runs; no usable profile gives NaN.

**Rationale:** [Käll, Krogh and Sonnhammer (2004), *A combined transmembrane topology and signal peptide prediction method*](https://sonnhammer.org/download/papers/2004_JMB_338%3A1027-1036.pdf) model SP regions and transmembrane segments together in Phobius. Their regional and length models motivate considering extent alongside peak height.

**Limitations:** the zero threshold is our fixed sign-based convention, not an optimized threshold or a measured h-region boundary. The paper also discusses artifacts in predicted length distributions; this descriptor is not a standalone SP/TM rule.

### 6. Small-residue enrichment after the peak

**Definition:** `postpeak_small_fraction` calculates the A/G/S fraction among canonical residues in the next 5 positions after the maximum window, stopping at position 40. No downstream positions gives 0; an available region containing only unknowns gives NaN. A missing peak also gives NaN.

**Rationale:** [Imai et al. (2011)](https://link.springer.com/article/10.1186/1471-2164-12-79) include an A/G/S c-region descriptor in their SP-related features.

**Limitations:** our anchor and region differ from theirs. The maximum window end is not assumed to be the h-region boundary. A zero for an empty downstream region records no observed small-residue content rather than a measured absence in a c-region.

### 7. Cleavage-motif compatibility

**Definition:** `cleavage_motif_score` scans candidate bonds from the maximum window end through position 40, requiring a following residue in the protein. For a bond after residue s (1-based), residues s − 2 and s correspond to −3 and −1. Each A/C/G/S/T contributes 0.5, and the largest score is retained. Sites with an unknown scored residue are skipped. No scorable bond gives 0; a missing peak gives NaN.

**Rationale:** [von Heijne (1984), *How signal sequences maintain cleavage specificity*](https://pubmed.ncbi.nlm.nih.gov/6423828/) describes positional preferences and the (−3, −1) rule, including eukaryotic sequences. [Bendtsen et al. (2004), *Improved prediction of signal peptides: SignalP 3.0*](https://services.healthtech.dtu.dk/services/SignalP-3.0/paper-3.0.pdf) also discuss cleavage-site preferences and combine position and composition inputs.

**Limitations:** our symmetric residue set and equal weights simplify the different positional preferences and additional constraints described in the literature. A score of 1 means two matches to our set, not a cleavage probability or a confirmed site; chance matches are possible. The score uses no annotated `cleavage_pos`, learned motif or PSWM from 03.

## Evaluation

We chose the regions, threshold, residue sets and score weights before model evaluation and kept them fixed. They are not extra grid dimensions. With D = 31, the existing grid gives k = 8, 16 and 31; C and gamma-factor choices are unchanged.

Feature ranking, scaling and parameter selection remain inside the current training subset. Any later comparison of feature sets or tuning of these definitions must use inner validation. The benchmarking split remains reserved, and no performance improvement is claimed before evaluation.
