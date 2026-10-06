# Laboratory of Bioinformatics 2 - Group 10

Project on signal-peptide prediction in eukaryotic proteins.

The main project notebooks correspond one-to-one with the course parts and use the same identifiers. Supplementary examples use an `_example` suffix.

## Repository structure

```text
LB2_project_Group_10/
|-- notebooks/
|   |-- 02a_data_collection.ipynb
|   |-- 02b_data_preparation.ipynb
|   |-- 02c_data_analysis.ipynb
|   |-- 03_von_heijne_example.ipynb
|   |-- 03_von_heijne_method.ipynb
|   `-- archive/
|       `-- Untitled2.ipynb
|-- data/
|   |-- collected/
|   |-- prepared/
|   `-- analysis/
|-- results/
|   `-- figures/
|       |-- 02c/
|       `-- 03/
|-- docs/
|   `-- notes.txt
|-- .gitignore
|-- requirements.txt
`-- README.md
```

- `notebooks/`: main notebooks for each course part and supplementary worked examples.
- `notebooks/archive/`: earlier drafts.
- `data/`: positive and negative datasets in TSV and FASTA formats.
- `data/collected/`: preliminary UniProt datasets.
- `data/prepared/`: representative sequences and metadata, including split and CV fold assignments.
- `data/analysis/`: cleavage-site FASTA windows for training and benchmarking.
- `results/figures/02c/`: exported data-analysis figures.
- `results/figures/03/`: PSWM and validation-score PDFs, numbered by subsection and CV round.
- `docs/`: project notes and documentation.

The plotting cells in 02c and 03 save each figure as a PDF, print its path and display it in the notebook. Rerunning a cell updates the corresponding file.

Python dependencies are listed in `requirements.txt`. Part 02b also requires the MMseqs2 command-line tool. Part 02c uses local WebLogo and requires Ghostscript for PDF and PNG output; its setup cell includes the Conda installation command.

## Progress

_Last updated: 6 October 2026._

**Current focus: [03 - Von Heijne method](notebooks/03_von_heijne_method.ipynb).** Data loading, fold selection, matrix construction and validation scoring are completed for the first CV round, using natural logarithms. The matrix heatmap and score histogram are saved as PDFs. Threshold optimization and full cross-validation remain pending.

| Part                                                         | Status      | Results                                                                                                |
| ------------------------------------------------------------ | ----------- | ------------------------------------------------------------------------------------------------------ |
| [02a - Data collection](notebooks/02a_data_collection.ipynb) | ✅ Reviewed | 2,957 positive and 20,974 negative proteins collected. |
| [02b - Data preparation](notebooks/02b_data_preparation.ipynb) | ✅ Reviewed | 1,102 positive and 9,082 negative representatives in four files. Training: 881 positive / 7,265 negative; benchmarking: 221 positive / 1,817 negative. Five training folds assigned. |
| [02c - Data analysis](notebooks/02c_data_analysis.ipynb) | 👀 Ready for review | Length, SP composition and taxonomy analyses completed, including frequent-species tables and observations. 16 numbered PDF figures exported, including local WebLogo cleavage-site logos for training and benchmarking with a shared axis and improved readability. Training N-terminal composition comparison completed with a 70-residue window. Observations describe shared cleavage-site preferences and upstream hydrophobic patterns in both splits. |
| [03 - Von Heijne method](notebooks/03_von_heijne_method.ipynb) | 🚧 In progress | First round: 528 training contexts, no incomplete-context exclusions and 1,629 validation proteins scored. Natural-log PSWM and two PDF figures saved. Threshold optimization and five-round evaluation pending. |

<details>
<summary>Status legend</summary>

- ⏳ **Pending:** not started.
- 🚧 **In progress:** work is underway.
- 👀 **Ready for review:** completed and checked by the group; awaiting the professor's review.
- ✅ **Reviewed:** reviewed by the professor, with no outstanding corrections.

Parts requiring corrections return to 🚧 **In progress**.

</details>
