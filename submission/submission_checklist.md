# Assignment 02 — evidence-based submission audit

Checked against professor's Assignment 02 deliverables. **Repository presence is not proof of end-to-end reproducibility or scientifically corrected data partitions.**

| Deliverable | Status | Evidence / qualification |
|---|---|---|
| Formal technical report | **Satisfied (file present)** | `report/Final_Report_ID22646206_Assignment_2.docx` (Word format; content and formatting not independently audited) |
| Complete source code | **Partial** | `notebooks/assignment02-final-implementation.ipynb` and `assignment02-final-analysis.ipynb` present; no clean rerun demonstrated |
| Datasets or official links | **Partial** | Candidate dataset publications documented; precise Kaggle source versions and selection differences unverified; raw files omitted |
| Merged dataset preparation code | **Not applicable** | Datasets evaluated independently |
| Experimental configuration files | **Partial** | `configs_and_manifests/` contains `dataset_splits.csv`, `retained_images.csv`, `training_eligible_images.csv`; exact weights, environment and per-run frozen config not independently recovered |
| Result tables and figures | **Satisfied (file presence)** | `Experiment_results/` holds 8 sets of test metrics, predictions, classification reports, and confusion matrices; `Figures/` holds 12 PNGs; summary CSV exists |
| Relevant training/testing logs | **Satisfied (file presence)** | `logs/` has Stage A and Stage B history CSVs for all 8 model-dataset pairs; test evidence in `Experiment_results/` |
| Selected-paper references | **Partial** | Included in Word report as supplied, but references and in-text match not fully audited |
| External-code/model acknowledgments | **Partial** | Original architecture and TorchVision cited in README; source of any adapted third-party code not fully checked |
| Reproducibility README | **Partial** | `README.md` documents workflow and findings, but exact runnable clean-environment commands cannot yet be verified |

## Important known limitations

- The report, notebook and figures should be independently cross-checked for figure labels, metric rounding and dataset naming.
- The current edited main notebook has not passed a fresh top-to-bottom execution.
- Checkpoint files are not hosted in this repository.
- Dataset-source DOI matches are *candidate provenance* until original Kaggle dataset versions and reduced image counts are explained.
- Original SHA-256 audit found 6,221 unique file hashes; image similarity investigations identified potential cross-partition lookalikes, which cannot be interpreted as confirmed duplicates nor ignored as a possible independence limitation.

## Contents verified via GitHub directory inventory

- Report: 1 DOCX.
- Notebook files: 2 IPYNB.
- Figures folder: 12 PNGs (4 comparisons and 8 learning-curve charts).
- Experiment results: 8 separate model-dataset test result folders, class reports, confusion matrices, metrics and predictions.
- Training logs: 16 history CSVs (2 training stages × 8 experiments).
- Configuration/manifests: 3 CSV files.
- `results/official_test_results.csv` and supplementary comparison outputs.

**Assessment:** Organized and substantially populated; do not label as fully submission-ready until mandatory partial items are resolved or formally acknowledged.
