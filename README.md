# Laboratory of Bioinformatics 2 - Group 10

Project on signal-peptide prediction in eukaryotic proteins.

The project notebooks correspond one-to-one with the course parts and use the same identifiers.

## Repository structure

```text
LB2_project_Group_10/
|-- notebooks/
|   |-- 02a_data_collection.ipynb
|   |-- 02b_data_preparation.ipynb
|   `-- archive/
|       `-- Untitled2.ipynb
|-- data/
|   |-- collected/
|   |   |-- positive_dataset.tsv
|   |   |-- positive_dataset.fasta
|   |   |-- negative_dataset.tsv
|   |   `-- negative_dataset.fasta
|   `-- prepared/
|       |-- positive_dataset.tsv
|       |-- negative_dataset.tsv
|       |-- positive_rep_seq.fasta
|       |-- negative_rep_seq.fasta
|       |-- positive_cluster.tsv
|       |-- negative_cluster.tsv
|       |-- positive_all_seqs.fasta
|       |-- negative_all_seqs.fasta
|       |-- training/
|       |   |-- positive_dataset.tsv
|       |   |-- positive_dataset.fasta
|       |   |-- negative_dataset.tsv
|       |   |-- negative_dataset.fasta
|       |   `-- cv_folds.tsv
|       `-- benchmarking/
|           |-- positive_dataset.tsv
|           |-- positive_dataset.fasta
|           |-- negative_dataset.tsv
|           `-- negative_dataset.fasta
|-- docs/
|   `-- notes.txt
|-- .gitignore
|-- requirements.txt
`-- README.md
```

- `notebooks/`: notebooks for each part of the project.
- `notebooks/archive/`: earlier drafts.
- `data/`: project datasets.
- `data/collected/`: preliminary UniProt datasets in TSV and FASTA formats.
- `data/prepared/`: MMseqs2 outputs, representative metadata and training/benchmarking datasets; temporary working directories are omitted from the tree.
- `docs/`: project notes and documentation.

Python dependencies are listed in `requirements.txt`. Part 02b also requires the MMseqs2 command-line tool.

## Progress

_Last updated: 21 September 2026._

**Current focus: [02b - Data preparation](notebooks/02b_data_preparation.ipynb).** Data preparation completed; ready for review.

| Part                                                         | Status      | Results                                                                                                |
| ------------------------------------------------------------ | ----------- | ------------------------------------------------------------------------------------------------------ |
| [02a - Data collection](notebooks/02a_data_collection.ipynb) | ✅ Reviewed | 2,957 positive and 20,974 negative proteins collected. |
| [02b - Data preparation](notebooks/02b_data_preparation.ipynb) | 👀 Ready for review | 1,102 positive and 9,082 negative representatives. Training: 881 positive / 7,265 negative; benchmarking: 221 positive / 1,817 negative. Five training folds assigned. |

<details>
<summary>Status legend</summary>

- ⏳ **Pending:** not started.
- 🚧 **In progress:** work is underway.
- 👀 **Ready for review:** completed and checked by the group; awaiting the professor's review.
- ✅ **Reviewed:** reviewed by the professor, with no outstanding corrections.

Parts requiring corrections return to 🚧 **In progress**.

</details>
