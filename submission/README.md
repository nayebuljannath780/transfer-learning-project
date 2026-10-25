# Advanced Machine Learning — Assignment 02

## Comparative Evaluation of Deep Transfer Learning Models for Rice Leaf Disease Classification

This is the submission-package preparation directory for a **dataset-based, two-dataset, four-architecture evaluation** continuing Assignment 01.

**Status:** This branch is a staging area, NOT a fully reproducible or submission-ready release. The actual Kaggle notebook and experiment archives must still be uploaded and checked.

### Selected architectures
- MobileNetV3-Large
- EfficientNet-B0
- EfficientNet-B3
- MobileNetV2

Eight official model/dataset experiments were completed, using independently initialized pretrained models. These are adaptations of existing architectures, not exact reproductions of published methods.

### Dataset partitions

| Dataset | Classes | Train | Validation | Test | Total |
|---|---:|---:|---:|---:|---:|
| D1 | 4 | 3372 | 739 | 683 | 4794 |
| D2 | 4 | 999 | 214 | 214 | 1427 |

D1 labels: Bacterialblight, Blast, Brownspot, Tungro.
D2 labels: Bacterial Leaf Blight, Brown Spot, Healthy Leaf, Tungro Virus.
Datasets were evaluated independently because their label definitions differ.

### Training
RGB images resized to 224×224; ImageNet normalization (mean 0.485, 0.456, 0.406; std 0.229, 0.224, 0.225). Training augmentation included horizontal and vertical flips, rotation up to 15 degrees, and modest brightness/contrast changes. Validation/test: no random augmentation.

- Stage A: frozen pretrained feature extractor; train classification head for 5 epochs with Adam, lr 1e-4
- Stage B: partially unfreeze later features, keep batch-normalization running statistics fixed; 3 epochs with Adam, lr 1e-5
- Batch size: 32; CrossEntropyLoss; seed: 42
- Checkpoints selected on validation macro-F1, not test results
- Training platform: Kaggle GPU / PyTorch; precise software versions and GPU model require checking against source logs

### Results

See [official_test_results.csv](results/official_test_results.csv). AUC means macro one-vs-rest ROC-AUC; all figures are rounded to 4 decimals. No literature scores are presented as new experiments.

### Data provenance and limitations

See [dataset_sources.md](datasets/dataset_sources.md). Candidate Mendeley sources have been identified but the direct provenance and the count differences still require verification against Kaggle input datasets and manifests.

SHA-256 checks of 6,221 files found no byte-identical duplicates. Separate image-similarity diagnostics identified potential cross-partition visually similar images, so complete split independence cannot be guaranteed from exact-hash testing alone. Preserve audit artifacts and interpret the results accordingly.

### How to reproduce

1. Obtain the actual cleaned Kaggle notebook `assignment02-final-implementation.ipynb` from the project's original experiment files.
2. Obtain the exact data versions used for D1/D2; reconstruct the saved split manifest.
3. Install the **actual dependencies and versions extracted from that notebook** (not yet recorded in this repository).
4. Configure Kaggle input dataset paths to match the attached dataset directories.
5. Run data preparation, Stage A, Stage B, and evaluation as implemented, ensuring the test split is not used for checkpoint selection.
6. Compare outputs with the recorded official results and logs. **No fresh end-to-end execution has yet been verified for the edited submission notebook.**

The source notebook, exact Kaggle input paths, checkpoints and logs must be uploaded before this guide can specify executable exact commands.

### Attribution

This work uses ImageNet-pretrained architectures from PyTorch TorchVision. Cite original architecture papers and any external code actually adapted, as well as verified source datasets and the rice-leaf research papers reviewed in Assignment 01. The final report's reference list must match these attributions.

### Submission contents

The professor requires: formal report; complete source code; dataset files when redistributable or official links; configuration files; results and figures; relevant training/testing logs; selected-paper references; external-code citations; a reproducibility README. Merged-dataset preparation does not apply here (the datasets were not merged).

See [submission_checklist.md](submission_checklist.md) for an evidence-based status review.
