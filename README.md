# Laboratory of Bioinformatics 2 - Group 10

Project on signal-peptide prediction in eukaryotic proteins.

The active project notebooks correspond one-to-one with the course parts and use the same identifiers. Supplementary notebooks provide worked examples and feature exploration.

## Repository structure

```text
LB2_project_Group_10/
|-- notebooks/
|   |-- 02a_data_collection.ipynb
|   |-- 02b_data_preparation.ipynb
|   |-- 02c_data_analysis.ipynb
|   |-- 03_von_heijne_method.ipynb
|   |-- 04_svm_method.ipynb
|   |-- 04_feature_exploration.ipynb
|   |-- 05_benchmarking_and_analysis.ipynb
|   |-- experiments/
|   |   |-- 04_svm_22/
|   |   |-- 04_svm_23_pswm/
|   |   `-- 04_svm_32_pswm/
|   `-- archive/
|-- data/
|   |-- collected/
|   |-- prepared/
|   `-- analysis/
|-- results/
|   |-- figures/
|   |   |-- 02c/
|   |   |-- 03/
|   |   |-- 04/
|   |   `-- 05/
|   `-- tables/
|       |-- 03/
|       |-- 04/
|       `-- 05/
|-- docs/
|   |-- 04_feature_candidates.md
|   `-- notes.txt
|-- .gitignore
|-- requirements.txt
`-- README.md
```

- `notebooks/`: main course notebooks and supplementary examples/exploration.
- [05 benchmarking and analysis](notebooks/05_benchmarking_and_analysis.ipynb): final-model training and benchmarking (0–3) are executed and internally reviewed; error analysis (4–6) remains pending.
- [04 feature exploration](notebooks/04_feature_exploration.ipynb): training profiles and distributions for the 11 non-composition SVM features, with observations.
- `notebooks/experiments/`: SVM variants, each with its own notebook, feature cache, tables and figures.
- `notebooks/archive/`: archived notebooks.
- `data/`: positive and negative datasets in TSV and FASTA formats.
- `data/collected/`: preliminary UniProt datasets.
- `data/prepared/`: representative sequences and metadata, including split and CV fold assignments.
- `data/analysis/`: cleavage-site FASTA windows for training and benchmarking.
- `results/figures/02c/`: exported data-analysis figures.
- `results/figures/03/`: PSWM, validation-score, precision–recall and CV evaluation PDFs.
- `results/tables/03/`: per-round CV results and metric summaries in TSV format.
- `results/figures/04/` and `results/tables/04/`: feature exploration, inner-search, feature-ranking and CV figures, with predictions and feature/metric tables.
- `results/tables/05/`: final predictors and training records, with accession-level benchmarking predictions and metrics.
- `results/figures/05/`: benchmarking confusion matrices and metric comparison PDFs.
- `docs/`: project notes and documentation.

The plotting cells save each figure as a PDF, print its path and display it in the notebook. Rerunning a cell updates the corresponding file.

Python dependencies are listed in `requirements.txt`. Part 02b also requires the MMseqs2 command-line tool. Part 02c uses local WebLogo and requires Ghostscript for PDF and PNG output; its setup cell includes the Conda installation command.

## SVM experiments

The variants use the same five training folds and fixed 27-candidate search, with k adjusted to the feature count. PSWM is fitted separately within each training subset. Values are mean ± SE across the outer folds. These runs evaluate the prediction procedures; selecting the final production model is a separate stage. Final benchmarking of the main predictors is reported in 05.

| Notebook | Features | MCC | F1 |
| --- | --- | --- | --- |
| [22-feature baseline](notebooks/experiments/04_svm_22/04_svm_22.ipynb) | 20 composition + 2 hydropathy | 0.803 ± 0.014 | 0.824 ± 0.012 |
| [23 features with PSWM](notebooks/experiments/04_svm_23_pswm/04_svm_23_pswm.ipynb) | Baseline + PSWM score | 0.850 ± 0.010 | 0.866 ± 0.008 |
| [32 features with PSWM](notebooks/experiments/04_svm_32_pswm/04_svm_32_pswm.ipynb) | Main 31 features + PSWM score | 0.887 ± 0.014 | 0.899 ± 0.012 |

## Progress

_Last updated: 30 October 2026._

**Current focus: [05 - Benchmarking and analysis of results](notebooks/05_benchmarking_and_analysis.ipynb).** Final-model training and benchmarking (0–3) completed and internally reviewed; error analysis (4–6) pending.

| Part                                                         | Status      | Results                                                                                                |
| ------------------------------------------------------------ | ----------- | ------------------------------------------------------------------------------------------------------ |
| [02a - Data collection](notebooks/02a_data_collection.ipynb) | ✅ Reviewed | 2,957 positive and 20,974 negative proteins collected. |
| [02b - Data preparation](notebooks/02b_data_preparation.ipynb) | ✅ Reviewed | 1,102 positive and 9,082 negative representatives in four files. Training: 881 positive / 7,265 negative; benchmarking: 221 positive / 1,817 negative. Five training folds assigned. |
| [02c - Data analysis](notebooks/02c_data_analysis.ipynb) | ✅ Reviewed | Length, SP composition and taxonomy analyses completed, including frequent-species tables and observations. 16 numbered PDF figures exported, including local WebLogo cleavage-site logos for training and benchmarking with a shared axis and improved readability. Training N-terminal composition comparison completed with a 70-residue window. Observations describe shared cleavage-site preferences and upstream hydrophobic patterns in both splits. |
| [03 - Von Heijne method](notebooks/03_von_heijne_method.ipynb) | ✅ Reviewed | Five-round test results (mean ± SE): MCC 0.667 ± 0.018; F1 0.703 ± 0.016; precision 0.665 ± 0.030; recall 0.751 ± 0.021; accuracy 0.931 ± 0.005. Six figures and two tables saved; observations completed. Final benchmarking reported separately in 05. |
| [04 - SVM method](notebooks/04_svm_method.ipynb) | 👀 Ready for review | Five outer rounds with 31 features and the fixed 27-candidate grid: MCC 0.858 ± 0.010; F1 0.873 ± 0.009 (mean ± SE). All 8,146 training proteins predicted once. Four figures and six result tables saved; observations completed. Final benchmarking reported separately in 05. |
| [05 - Benchmarking and analysis of results](notebooks/05_benchmarking_and_analysis.ipynb) | 🚧 In progress | Sections 0–3 executed and internally reviewed. On 2,038 benchmark proteins: MCC/F1 = 0.663/0.700 (von Heijne), 0.871/0.885 (31-feature SVM). Eight TSVs, one predictor pickle and two PDFs saved; error analysis (4–6) pending. |

<details>
<summary>Status legend</summary>

- ⏳ **Pending:** not started.
- 🚧 **In progress:** work is underway.
- 👀 **Ready for review:** completed and checked by the group; awaiting the professor's review.
- ✅ **Reviewed:** reviewed by the professor, with no outstanding corrections.

Parts requiring corrections return to 🚧 **In progress**.

</details>
