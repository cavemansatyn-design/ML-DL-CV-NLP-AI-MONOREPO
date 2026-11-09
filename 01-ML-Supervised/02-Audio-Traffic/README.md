# 01.2 — Audio and Traffic Prediction

Two supervised-learning notebooks share the Assignment 3 data archive. Their report records data analysis, model comparisons, error diagnostics and validation choices.

## Dataset dependency

Both notebooks expect `ML_A3.zip` in this folder and extract its contents during setup. The archive should contain:
- `partA_train.csv`
- `partA_val.csv`
- `partB_clf_train.csv`
- `partB_clf_val.csv`
- `partB_reg_train.csv`
- `partB_reg_val.csv`
- the corresponding audio `.wav` clips

**The uploaded source ZIP inspected for this build did not contain `ML_A3.zip`.** The notebook and PDF report are preserved, but a clean rerun of these two notebooks is blocked until the original archive is added here.

## A. Speaker-independent spoken-digit recognition

File: `spoken-digit-svm (ML_A3.zip).ipynb`

### Data and problem setup
- Training: 2,000 clips and 53 acoustic features, with speakers S1–S4.
- Validation: 500 clips from a fifth, unseen speaker S5; 50 clips per digit.
- Audio is mono, sampled at 8 kHz, with clip durations reported from 0.22 to 1.00 seconds.
- Feature standard deviations range from 0.1530 to 44.8118, making scaling important for an RBF kernel.

### Validation strategy
| Scheme | Accuracy | Interpretation |
|---|---:|---|
| Stratified 5-fold CV | 90.50% ± 0.96% | Randomly mixes speakers across folds; speaker leakage makes it optimistic |
| Leave-One-Speaker-Out CV | 50.85% | Holds out a speaker; better proxy for unseen-speaker generalisation |
| S5 validation file | 73.00% | Direct evaluation on a separate unseen speaker |

The notebook explicitly identifies LOSO as the better model-selection guide because the deployment setting involves speakers absent from training.

### Standardisation and feature selection
- RBF SVM with `StandardScaler`: S5 accuracy **73.00%**.
- RBF SVM without standardisation: **17.20%**.
- A digit-to-speaker ANOVA F-statistic ratio ranks features by phonetic relevance relative to speaker dependence.
- The top 34 of 53 features are retained; 19 are dropped.
- The selected-feature model reports S5 accuracy **82.00%**, an absolute gain of **9 percentage points** over the standardised all-feature model.
- Selected-feature LOSO accuracy is reported as 49.50%; therefore the held-out S5 score and cross-speaker CV estimate are not identical.

### Error analysis
- 135 of 500 validation clips are misclassified by the 73%-accuracy model.
- Reported difficult digits include 0 (20% per-digit accuracy) and 8 (34%); digits 1 and 6 reach 98%.
- The notebook inspects five misclassified clips and discusses low recording level, silence, truncation and pitch/formant variation.
- The report predicts 80–82% hidden-test accuracy, but this is a forecast, not a measured test result.

### Limitations
Microphone frequency response and room reverberation may differ between speakers/recording environments. The report proposes cepstral mean normalisation and room-impulse-response augmentation as future improvements.

## B. Traffic-volume prediction and traffic-level classification

File: `traffic-prediction (ML_A3.zip).ipynb`

### Data quality and leakage checks
- Training data: 34,170 rows.
- `f12` contains 10 impossible values of −363.57 K; `f5` contains an extreme rainfall value of 6,849.467 mm.
- `f6` has 1,678 missing values (4.91%); `f12` has 2,993 (8.76%).
- `f8` is a unique row identifier (34,170 unique values).
- `f7` has disjoint train and validation ranges, consistent with a future-period holdout.
- The notebook treats row ID, time counter and uninformative/noisy columns carefully to reduce leakage and spurious splits.

### Regression validation
| Validation scheme | R² |
|---|---:|
| Random 5-fold | 0.9325 ± 0.0031 |
| TimeSeriesSplit (5 folds) | 0.9232 ± 0.0066 |
| Out-of-time validation | 0.8025 |

The out-of-time score is the most relevant estimate for future-period prediction. Random folds can place temporally adjacent examples on both sides of a split.

### Model experiments
- Linear Regression baseline: validation R² **0.1574**.
- Single decision tree: validation R² peaks at **0.9055** at depth 7; deeper trees overfit.
- Bagging and Random Forest experiments compare 10, 30, 50 and 100 trees.
- Gradient Boosting reaches validation R² **0.8796** in the displayed 100-estimator, learning-rate 0.1 comparison.
- Cleaning and feature ablation results: raw/native-NaN 0.8703; raw/median-imputed 0.8610; sensor-cleaned 0.8797; selected feature pipeline 0.9395.
- Final notebook output: **validation R² = 0.9399** and **validation macro-F1 = 0.8694**.

### Traffic-level classification
| Input set | Decision Tree macro-F1 | SVM macro-F1 |
|---|---:|---:|
| Raw features | 0.8330 | 0.5541 |
| Clean features | **0.8722** | 0.6550 |

The final classification macro-F1 output is 0.8694. The feature-importance analysis identifies `f14` and `f11` as the dominant variables in the reported comparison.

## Interpretation
These are results on the notebook's validation design. In particular, the 0.9399 R² final output should not be confused with the stricter out-of-time score of 0.8025; the validation protocol determines what generalisation claim is justified.
