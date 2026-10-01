# Evaluating Localization, Attribution, and External Generalization in Ground-Truth-Localized Breast Ultrasound Lesion Classification

This repository contains the frozen, publication-oriented analysis code for a study of breast ultrasound lesion classification under controlled localization, attribution, preprocessing, and external-validation conditions.

## Study scope

The classifier is a **ground-truth-assisted lesion classifier**. Lesion masks are used to construct the model input ROI; the system is therefore **not an end-to-end lesion detector plus classifier** and should not be interpreted as a clinical diagnostic system.

The primary internal cohort contains 647 BUSI benign/malignant images (437 benign, 210 malignant), with a locked 455/96/96 train/validation/test split. Exact duplicate images are controlled using MD5-based split groups. Patient-level independence could not be independently verified from the available BUSI identifiers.

The external evaluation uses 252 binary BrEaST-Lesions-USG cases (154 benign, 98 malignant), with the frozen Pass 3B raw-ROI model evaluated zero-shot at threshold 0.50 without retraining, fine-tuning, threshold optimization, or calibration.

## Main analyses

| Notebook | Analysis |
|---|---|
| `01_pass3a_publication_baseline_audit.ipynb` | BUSI inventory, duplicate, mask, and identifier audit |
| `02_pass3b_locked_vgg16_baseline.ipynb` | Locked split and VGG16 whole-image/raw-ROI/preprocessed-ROI baseline |
| `03_pass4_localization_robustness.ipynb` | Controlled ±5%, ±10%, ±15% localization perturbations |
| `04_pass5_gradcam_bootstrap_correction.ipynb` | Corrected 96-image Grad-CAM bootstrap analysis |
| `05_pass6a_breast_dataset_audit.ipynb` | BrEaST image/mask/dataset-level audit |
| `06_pass6b_breast_zero_shot_external_validation.ipynb` | Zero-shot external discrimination and calibration |
| `07_pass7_preprocessing_ablation.ipynb` | Raw, Min-Max, CLAHE, and Min-Max+CLAHE ablation |
| `08_pass8_publication_synthesis.ipynb` | Cross-pass integrity checks, tables, figures, and manuscript text |

## Key findings

- Whole-image BUSI classification: ROC-AUC 0.810, sensitivity 0.387.
- Ground-truth raw-ROI baseline: ROC-AUC 0.998, sensitivity 0.903 on the locked internal test set.
- Localization perturbation experiments retained high performance under the specific simulated geometric errors evaluated.
- Grad-CAM showed partial spatial correspondence: 31.8% of activation mass was within the annotated lesion overall; thresholded attribution IoU was 0.049 and lesion coverage was 0.056 at the primary threshold.
- Preprocessing produced comparatively small changes in discrimination; Min-Max normalization modestly improved Brier score and log loss relative to the independently fitted Pass 7 raw-ROI model.
- Zero-shot BrEaST evaluation: ROC-AUC 0.836 (95% CI 0.783–0.884), sensitivity 0.745, specificity 0.805, balanced accuracy 0.775, PR-AUC 0.776.
- External probability calibration was imperfect (Brier score 0.164; log loss 0.502).

These results are deliberately interpreted within the scope of a ground-truth-localized retrospective classification study.

## Data

The image datasets are **not included** in this repository.

### BUSI

Obtain the BUSI dataset from its original publication/source and place the files under:

```text
data/Dataset_BUSI_with_GT/
├── benign/
├── malignant/
└── normal/
```

The classification experiments use benign and malignant cases; normal cases are excluded from the binary classification cohort.

### BrEaST-Lesions-USG

Obtain the BrEaST-Lesions-USG data and accompanying metadata from the original source. Place the metadata workbook at:

```text
data/metadata/BrEaST_metadata.xlsx
```

The dataset itself is not redistributed here.

## Reproducibility

Use Python 3.10–3.12 and install the dependencies in `requirements.txt`.

Run the notebooks in numerical order:

```text
01 → 02 → 03 → 04 → 05 → 06 → 07 → 08
```

The intended execution flow and model lineage are documented in `docs/REPRODUCIBILITY.md`. Raw medical image data and machine-specific artifacts are excluded by `.gitignore`.

## Citation

See `CITATION.cff` for software citation metadata.

## License

The repository code and documentation are released under the MIT License. Dataset licensing remains governed by the original dataset providers.
