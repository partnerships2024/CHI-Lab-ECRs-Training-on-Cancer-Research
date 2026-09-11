# PanTS: Pancreatic Tumor Segmentation — Model Submission

This package contains the submission materials for evaluation on the PanTS benchmark.

The official PanTS repository defines **PanTS-te (n=901)** as the official in-distribution test set and requests model submissions to include a model checkpoint, testing script, in-distribution test results, and a brief README with usage instructions.

## Submission Contents

```text
PanTS_submission/
├── README.md
├── test.py
├── requirements.txt
├── checkpoints/
│   └── pants_best.pth
└── results/
    └── in_distribution_results.csv
```

> **Important:** `checkpoints/pants_best.pth` is a placeholder file path. Replace it with your actual trained checkpoint before submission. Likewise, replace the placeholder test results with the actual results obtained on PanTS-te.

## 1. Model Checkpoint

Place the trained model checkpoint at:

```text
checkpoints/pants_best.pth
```

The checkpoint should be the model used to produce the reported PanTS-te results.

## 2. Testing Script

The supplied `test.py` provides a command-line inference/evaluation interface:

```bash
python test.py \
    --checkpoint checkpoints/pants_best.pth \
    --data_dir /path/to/test/data \
    --output_dir predictions
```

For an actual submission, update the model-loading and preprocessing sections of `test.py` to exactly match the architecture and preprocessing used during training.

## 3. In-Distribution Test Results

The official PanTS in-distribution test set is **PanTS-te (n=901)**.

Report the actual results obtained on PanTS-te in:

```text
results/in_distribution_results.csv
```

Recommended benchmark metrics include:

- Patient-wise sensitivity (P-Sen)
- Tumor-wise sensitivity (T-Sen)
- Specificity (Spe)
- AUC
- Dice similarity coefficient (DSC)

Do not submit placeholder values. Replace the values in the CSV with the actual evaluation results.

## 4. Environment

Example environment:

```text
Python >= 3.10
PyTorch
MONAI
NumPy
nibabel
SimpleITK
scikit-learn
```

Install dependencies with:

```bash
pip install -r requirements.txt
```

## 5. Expected Data

The test script expects a directory containing the test images and, when evaluating locally, corresponding ground-truth masks.

Example:

```text
test_data/
├── images/
│   ├── case_001.nii.gz
│   ├── case_002.nii.gz
│   └── ...
└── masks/
    ├── case_001.nii.gz
    ├── case_002.nii.gz
    └── ...
```

Adapt the data-loading section of `test.py` if the actual PanTS data organisation differs.

## 6. Output

Predictions are written to the directory specified by `--output_dir`.

Example:

```text
predictions/
├── case_001.nii.gz
├── case_002.nii.gz
└── ...
```

Evaluation results are saved under:

```text
results/
```

## 7. External/OOD Evaluation

The PanTS team requests submitted models for external evaluation. The JHU team performs evaluation on external datasets, so the submitted inference code should not depend on hard-coded filenames or local paths.

The official PanTS README states that external evaluation includes proprietary UCSF, Polish, and Peking University pancreatic datasets, as well as the RSNA Abdominal Trauma Detection Dataset.

## 8. Reproducibility

To reproduce the submitted results:

1. Install the required packages.
2. Place the trained checkpoint in `checkpoints/`.
3. Prepare the PanTS-te test data.
4. Run `test.py`.
5. Compare the generated metrics with `results/in_distribution_results.csv`.

## Submission Checklist

- [ ] Actual trained model checkpoint included
- [ ] Testing script tested successfully
- [ ] PanTS-te in-distribution results included
- [ ] No placeholder metrics remain
- [ ] README updated with actual model architecture and preprocessing
- [ ] Dependencies documented
- [ ] No hard-coded local file paths

## Reference

PanTS: The Pancreatic Tumor Segmentation Dataset, Johns Hopkins University, NeurIPS 2025.

Official repository:
https://github.com/MrGiovanni/PanTS
