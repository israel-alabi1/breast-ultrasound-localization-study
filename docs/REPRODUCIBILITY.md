# Reproducibility

The publication analysis is frozen at Pass 8.

## Execution order

01 → 02 → 03 → 04 → 05 → 06 → 07 → 08

Pass 3B creates the locked 455/96/96 BUSI split using MD5 exact-duplicate groups. This controls exact-image duplication leakage; it does not establish patient-level independence.

Pass 3B is the baseline model lineage used for BrEaST zero-shot evaluation. Pass 7 contains separate raw-ROI, Min-Max, CLAHE, and Min-Max+CLAHE fits and must not be substituted for the Pass 3B external-validation model.

Images are scaled approximately to [0,1] in the implemented experiments; canonical VGG16 preprocess_input is not used.

The external BrEaST evaluation is zero-shot: no retraining, fine-tuning, threshold optimization, or calibration is performed.

For publication results, preserve the frozen outputs and do not silently overwrite them by rerunning training with a changed stochastic implementation.
