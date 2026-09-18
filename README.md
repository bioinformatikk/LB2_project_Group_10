# Laboratory of Bioinformatics 2 - Group 10

Project on signal-peptide prediction in eukaryotic proteins.

## Repository structure

```text
LB2_project_Group_10/
|-- notebooks/
|   |-- 02a_data_collection.ipynb
|   `-- archive/
|       `-- Untitled2.ipynb
|-- data/
|   `-- collected/
|       |-- positive_dataset.tsv
|       |-- positive_dataset.fasta
|       |-- negative_dataset.tsv
|       `-- negative_dataset.fasta
|-- docs/
|   `-- notes.txt
|-- requirements.txt
`-- README.md
```

- **notebooks/**: project notebooks named with the matching course-material identifier. Start with [02a_data_collection.ipynb](notebooks/02a_data_collection.ipynb).
- **notebooks/archive/**: earlier drafts kept for reference. These are not part of the current workflow; their original output paths have not been adapted.
- **data/collected/**: preliminary UniProt datasets after the collection filters. These are not raw API responses and have not yet been prepared for cross-validation or independent testing.
- **docs/**: project notes and documentation. `notes.txt` is the placeholder retained from the original layout. Course PDFs and example notebooks are stored separately in the course materials folder.

## Course correspondence

| Course part | Topic | Project notebook |
| --- | --- | --- |
| 01a | Introduction | Reference material; no project notebook yet |
| 01b | VM setup | Reference material; no project notebook yet |
| 01c | Biological background: signal peptides | Reference material; no project notebook yet |
| 02a | Data collection | [02a_data_collection.ipynb](notebooks/02a_data_collection.ipynb) |
| 02b | Data preparation | Planned: `02b_data_preparation.ipynb` |

The course examples `02a-1`, `02a-2`, and `02a-3` are supporting notebooks for part `02a`, not additional project stages. Future notebooks will take their identifiers from the corresponding published course materials. No empty notebooks are created for planned parts.

Course sources: [materials folder](https://drive.google.com/drive/folders/1xbRIFUsTe_itxZ9DliIfeOUEwHP8G0Ik), [Data Collection](https://drive.google.com/file/d/18otuH3ur6PAnyMFNig8FE0P8ItZG6isk/view), and [Data Preparation](https://drive.google.com/file/d/1_eOR563uNTlKtRRKHji-H8R2iGS3VfEA/view).

## Run data collection

Use Python 3 with a Jupyter-compatible editor, such as VS Code with the Jupyter extension, or JupyterLab. Install the notebook dependency in the selected kernel environment:

```sh
python -m pip install -r requirements.txt
```

Open `notebooks/02a_data_collection.ipynb` and run its cells from top to bottom. Internet access is required for UniProt requests. The working directory must be inside this repository; both the repository root and `notebooks/` are supported.

The notebook writes both TSV metadata and full-sequence FASTA files to `data/collected/`. Running it again overwrites these files. Existing datasets remain available without rerunning the download.

## Organization conventions

- Match each notebook to its course part: `02a_data_collection.ipynb` follows `02a-DataCollection-2026.pdf`; `02b_data_preparation.ipynb` will follow `02b-DataPreparation-2026.pdf`. Keep the course number and letter; do not assign independent execution numbers.
- Keep earlier drafts in `notebooks/archive/` and use the numbered notebooks for current work.
- Keep collection outputs in `data/collected/`. Add `data/processed/` when preprocessing produces new datasets, preserving the collection outputs.
- Add `results/` for generated tables, figures, and evaluation outputs when those stages are implemented; use `docs/` for written notes.
- Keep Python dependencies in `requirements.txt`. Notebook checkpoints, virtual environments, and Python caches are excluded from Git.
- Review dataset changes before committing: a fresh UniProt download can change both annotations and record counts.
