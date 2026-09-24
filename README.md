# Laboratory of Bioinformatics 2 - Group 10

Project on signal-peptide prediction in eukaryotic proteins.

The project notebooks correspond one-to-one with the course parts and use the same identifiers.

## Repository structure

```text
LB2_project_Group_10/
|-- notebooks/
|   |-- 02a_data_collection.ipynb
|   |-- 02b_data_preparation.ipynb
|   |-- 02c_data_analysis.ipynb
|   `-- archive/
|       `-- Untitled2.ipynb
|-- data/
|   |-- collected/
|   `-- prepared/
|-- docs/
|   `-- notes.txt
|-- .gitignore
|-- requirements.txt
`-- README.md
```

- `notebooks/`: notebooks for each part of the project.
- `notebooks/archive/`: earlier drafts.
- `data/`: positive and negative datasets in TSV and FASTA formats.
- `data/collected/`: preliminary UniProt datasets.
- `data/prepared/`: representative sequences and metadata, including split and CV fold assignments.
- `docs/`: project notes and documentation.

Python dependencies are listed in `requirements.txt`. Part 02b also requires the MMseqs2 command-line tool.

## Progress

_Last updated: 24 September 2026._

**Current focus: [02c - Data analysis](notebooks/02c_data_analysis.ipynb).** Step 1: compare length distributions.

| Part                                                         | Status      | Results                                                                                                |
| ------------------------------------------------------------ | ----------- | ------------------------------------------------------------------------------------------------------ |
| [02a - Data collection](notebooks/02a_data_collection.ipynb) | ✅ Reviewed | 2,957 positive and 20,974 negative proteins collected. |
| [02b - Data preparation](notebooks/02b_data_preparation.ipynb) | ✅ Reviewed | 1,102 positive and 9,082 negative representatives in four files. Training: 881 positive / 7,265 negative; benchmarking: 221 positive / 1,817 negative. Five training folds assigned. |
| [02c - Data analysis](notebooks/02c_data_analysis.ipynb) | 🚧 In progress | Protein and SP length plots completed, with P99 views and descriptive observations. Figure selection pending. |

<details>
<summary>Status legend</summary>

- ⏳ **Pending:** not started.
- 🚧 **In progress:** work is underway.
- 👀 **Ready for review:** completed and checked by the group; awaiting the professor's review.
- ✅ **Reviewed:** reviewed by the professor, with no outstanding corrections.

Parts requiring corrections return to 🚧 **In progress**.

</details>
