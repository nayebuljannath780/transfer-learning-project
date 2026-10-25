# Assignment 02 — Rice Leaf Disease Classification

**Project:** Comparative Evaluation of Deep Transfer Learning Models for Rice Leaf Disease Classification  
**Course:** Advanced Machine Learning · Assignment 02  
**Experimental option:** Dataset-based evaluation (four models × two separate datasets)

This directory contains the recorded implementation, report, figures, test outputs, split manifests, and training histories for eight experiments. **The uploaded files are present; a fresh end-to-end reproducibility run of the edited notebook has not been verified.**

## Where everything is

| Component | Actual path |
|---|---|
| Technical report (editable Word document) | [report/Final_Report_ID22646206_Assignment_2.docx](report/Final_Report_ID22646206_Assignment_2.docx) |
| Training / evaluation source notebook | [notebooks/assignment02-final-implementation.ipynb](notebooks/assignment02-final-implementation.ipynb) |
| Analysis notebook | [notebooks/assignment02-final-analysis.ipynb](notebooks/assignment02-final-analysis.ipynb) |
| Official rounded comparison CSV | [results/official_test_results.csv](results/official_test_results.csv) |
| Eight folders with test metrics, predictions, class reports and confusion matrices | [Experiment_results/](Experiment_results/) |
| Twelve figures (four comparisons; eight learning curves) | [Figures/](Figures/) |
| Stage A and Stage B training histories (eight model–dataset pairs) | [logs/](logs/) |
| Split and image selection manifests | [configs_and_manifests/](configs_and_manifests/) |
| Source attribution and dataset provenance status | [datasets/dataset_sources.md](datasets/dataset_sources.md) |

Some comparison PNGs and CSVs also occur in `Experiment_results/Assignment02_Final_Comparisons/`; `Figures/` is the figure collection intended for the report.

## Models and datasets

Four ImageNet-pretrained convolutional architectures were adapted with four-class classification heads: **MobileNetV3-Large, EfficientNet-B0, EfficientNet-B3, MobileNetV2**. Each architecture was initialized independently for each dataset; these experiments do **not** reproduce an entire paper-specific methodology.

| Dataset | Class labels | Train | Validation | Test | Total |
|---|---|---:|---:|---:|---:|
| D1 | Bacterialblight; Blast; Brownspot; Tungro | 3,372 | 739 | 683 | 4,794 |
| D2 | Bacterial Leaf Blight; Brown Spot; Healthy Leaf; Tungro Virus | 999 | 214 | 214 | 1,427 |

Label definitions differ: **the datasets were not merged**, and model comparisons are made within each dataset. The saved `dataset_splits.csv` should be used to reconstruct the same partitions.

### Dataset sources

Candidate upstream records (not conclusively traced to the precise Kaggle downloads and experimental subsets):
- D1 candidate: P. K. Sethy, *Rice Leaf Disease Image Samples*, Mendeley Data v2, https://doi.org/10.17632/fwcj7stb8r.2
- D2 candidate: S. A. Rimi and M. J. U. Chowdhury, *RiceLeafBD*, Mendeley Data v1, https://doi.org/10.17632/kx9rx8p2mz.1

See [datasets/dataset_sources.md](datasets/dataset_sources.md) for the unresolved provenance and image-count reconciliation. The Kaggle input titles previously observed were `Rice Leaf Disease Images` and `RiseDisease`; verify their precise download/version links before claiming provenance. Original raw images are **not** hosted in this repository. Confirm license and any required attribution before redistribution.

## Data and training protocol

- Image conversion: RGB; resize to 224 × 224
- ImageNet normalization mean `(0.485, 0.456, 0.406)`; standard deviation `(0.229, 0.224, 0.225)`
- Training augmentation: random horizontal/vertical flips, rotations up to 15°, modest brightness/contrast adjustments
- Validation/test: resize and normalization without random augmentation
- **Stage A:** pretrained feature extractor frozen; train new classifier; 5 epochs; Adam, learning rate `1e-4`
- **Stage B:** partially unfreeze selected later feature layers; hold pretrained batch-normalization running statistics fixed; 3 epochs; Adam, learning rate `1e-5`
- Batch size 32; cross-entropy loss; seed 42
- Best checkpoint based on **validation macro-F1**, not test performance
- Environment: Kaggle GPU with PyTorch/TorchVision. Exact runtime image, GPU, dependency versions, and pretrained weight identifiers require source-environment confirmation.

## Evaluation and recorded test results

All precision, recall, and F1 values below are **macro-averaged**; AUC is **macro one-vs-rest**. Values displayed to four decimal places. For full-precision scores, class-wise reports, confusion matrices and predictions, use `Experiment_results/`.

| Model | Dataset | Accuracy | Macro precision | Macro recall | Macro F1 | Macro OvR AUC |
|---|---|---:|---:|---:|---:|---:|
| MobileNetV3-Large | D1 | 0.9971 | 0.9976 | 0.9965 | 0.9971 | 1.0000 |
| MobileNetV3-Large | D2 | 0.9159 | 0.9211 | 0.9235 | 0.9222 | 0.9851 |
| EfficientNet-B0 | D1 | 0.9854 | 0.9849 | 0.9844 | 0.9846 | 0.9989 |
| EfficientNet-B0 | D2 | 0.8411 | 0.8693 | 0.8601 | 0.8569 | 0.9701 |
| EfficientNet-B3 | D1 | 0.9883 | 0.9875 | 0.9875 | 0.9875 | 0.9992 |
| EfficientNet-B3 | D2 | 0.8785 | 0.8929 | 0.8788 | 0.8852 | 0.9748 |
| MobileNetV2 | D1 | 0.9722 | 0.9710 | 0.9734 | 0.9720 | 0.9986 |
| MobileNetV2 | D2 | 0.8692 | 0.8835 | 0.8802 | 0.8795 | 0.9737 |

`1.0000` AUC is rounded; it is not proof of an exactly perfect underlying AUC.

## How to inspect or reproduce

1. Open [the implementation notebook](notebooks/assignment02-final-implementation.ipynb) in a compatible Jupyter or Kaggle Python environment. The [analysis notebook](notebooks/assignment02-final-analysis.ipynb) is an additional artifact, not a replacement for the implementation.
2. Attach the **exact source datasets used in the experiment**, after confirming source versions and licensing. Match the data paths expected by the notebook; Kaggle `/kaggle/input/` paths may need adjustment in a different environment.
3. Reconstruct the retained image selection and D1/D2 partitions using `configs_and_manifests/`. **Do not re-randomize the test split.**
4. Check Python, PyTorch, TorchVision, scikit-learn, Pillow, and other imported packages against the actual notebook before installing version-specific dependencies. A frozen environment/requirements lockfile has not been verified or added.
5. Inspect the execution order and notebook-specific paths before running from a clean environment. The original eight experiments were already completed, but **the edited submission notebook has not been confirmed to run end-to-end**.
6. For inference/evaluation from saved checkpoints, obtain the selected weights from the original Kaggle experiment archives. Weights are **not present in this GitHub repository**. Loading checkpoints and invoking evaluation require the original code's paths and settings.
7. Compare any rerun outputs with `Experiment_results/`, `logs/`, and `results/official_test_results.csv`. Do not use the test data for tuning or checkpoint selection.

**Limitations:** 6,221 images had distinct SHA-256 hashes (no byte-identical duplicates). A supplementary image-similarity check found *potential* visually similar cross-partition images; this is an unresolved independence limitation, not proof of confirmed leakage. Preserve the audit evidence and do not claim a proven leakage-free split.

## Attribution

- Original architectures: Howard et al., *Searching for MobileNetV3* (ICCV 2019); Tan and Le, *EfficientNet* (ICML 2019); Sandler et al., *MobileNetV2* (CVPR 2018).
- Framework and pretrained weights: [PyTorch](https://pytorch.org/) and [TorchVision pretrained models](https://docs.pytorch.org/vision/main/models).
- Rice leaf disease research reviewed in Assignment 01: see the report's reference section.
- External code: any copied or adapted repository-specific code must be cited individually after confirming its origin; this has not been fully audited.

## Submission audit

The repository now includes report, notebooks, test result folders, figures, training histories and manifests. **Dataset download provenance, environment lockfile, exact replay instructions, external code attribution, and unhosted checkpoints remain unverified or incomplete.** This README deliberately does not claim the package is fully reproducible.
