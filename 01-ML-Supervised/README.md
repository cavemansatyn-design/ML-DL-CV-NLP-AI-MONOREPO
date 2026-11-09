# 01 — Supervised Machine Learning

This section contains two classification/regression groups: conventional tabular modelling and audio/traffic prediction.

## 01.1 — Classification and regression

See [01-Classification-Regression](01-Classification-Regression/README.md).
- `logistic-regression-breast-cancer.ipynb` — logistic-regression MLE/MAP and breast-cancer diagnostic classification.
- `regression-models (train.csv).ipynb` — EDA, missing-data handling, encoding, group-aware validation, linear/regularised regression and histogram gradient boosting.
- `train.csv` — regression dataset.
- `regression-report.pdf` — supporting regression report.

**Regression headline:** Histogram Gradient Boosting validation R² 0.8802, RMSE 221.22, MAE 154.84; Linear Regression validation R² 0.7543, RMSE 316.87, MAE 233.30.

## 01.2 — Audio and traffic prediction

See [02-Audio-Traffic](02-Audio-Traffic/README.md).
- `spoken-digit-svm (ML_A3.zip).ipynb` — speaker-independent spoken digit recognition.
- `traffic-prediction (ML_A3.zip).ipynb` — traffic-volume regression and traffic-level classification.
- `audio-traffic-report.pdf` — detailed results and analysis.

**Important dataset status:** `ML_A3.zip` is not included in the uploaded archive used to create this repository. Place the original archive in `02-Audio-Traffic/` before rerunning these notebooks. Do not replace it with an unrelated CSV or rename a different archive to this name.

## Evaluation principles

The notebooks demonstrate why the validation design must match the data-generating structure:
- group-aware validation for related regression rows;
- speaker-held-out validation for audio;
- out-of-time validation for traffic.

All numbers in the READMEs are validation results from the supplied report/notebook, not hidden-test results.
