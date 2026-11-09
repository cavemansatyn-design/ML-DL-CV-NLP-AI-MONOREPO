# 02 — Unsupervised Machine Learning

One notebook contains three practicals. The notebook is intentionally kept whole because the original assignment groups these experiments together. It covers numeric clustering, geographic clustering and text-document clustering.

## Notebook and data
`clustering-lab (penguins.csv, airbnb_nyc.csv, newsgroups.csv).ipynb`

| Dataset | Role | Observations |
|---|---|---:|
| `penguins.csv` | Numeric clustering of penguin measurements | 344 |
| `airbnb_nyc.csv` | Spatial clustering of NYC listing coordinates | 30,555 |
| `newsgroups.csv` | NLP document clustering | 2,000 |

All three CSV files are stored beside the notebook. `clustering-report.pdf` is included as the companion report.

## 1. Palmer Penguins — K-Means and Gaussian Mixture Models

### Preparation
- Uses four numeric measurements: bill length, bill depth, flipper length and body mass.
- The dataset contains 344 observations.
- Each selected feature has two missing values; two rows contain at least one missing selected measurement.
- Features are standardised before distance-based modelling.

### K-Means
| K | Silhouette |
|---:|---:|
| 2 | **0.5307** |
| 3 | 0.4443 |
| 4 | 0.3976 |
| 5 | 0.3759 |
| 6 | 0.3670 |

K=2 is selected by the highest tested silhouette score. The resulting cluster sizes are 123 and 221.

### Gaussian Mixture Model
The notebook compares component counts and covariance structures using AIC/BIC. The selected configuration is **K=4 with tied covariance**, chosen by the lowest BIC among the tested configurations. It converges; the fitted model reports 8 EM iterations. The notebook also records 29 trace iterations for the displayed likelihood trace.

### External comparison with species
| Model | ARI | NMI |
|---|---:|---:|
| K-Means (K=2) | 0.6456 | 0.7467 |
| GMM (K=4, tied) | **0.7484** | **0.8168** |

ARI and NMI compare discovered clusters with known species labels after clustering. They are external evaluation metrics; species labels are not used as supervised training targets.

## 2. NYC spatial clustering — K-Means and DBSCAN

- Loads 30,555 latitude/longitude observations; the reported coordinate columns have no missing values.
- K-Means uses K=5 and assigns all 30,555 observations. Cluster sizes are 2,155; 11,440; 8,298; 2,971; and 5,691.
- DBSCAN explores distance-based neighbourhood sizes and reports a selected epsilon of **0.35 km**.
- At epsilon 0.35 km, **1,624 points (5.315%)** are labelled noise.
- Sensitivity comparison:
  - epsilon 0.20 km: 4,264 noise points (13.955%);
  - epsilon 0.35 km: 1,624 (5.315%);
  - epsilon 0.50 km: 718 (2.350%).

The epsilon experiment demonstrates the density/noise trade-off: increasing the neighbourhood radius reduces the number of observations labelled as noise. Geographic coordinates require distance-aware treatment; the notebook expresses DBSCAN's neighbourhood scale in kilometres.

## 3. NLP — Newsgroups document clustering

This is the NLP component of the repository. It is classified here because the task is unsupervised document clustering rather than supervised text classification.

### Representation
- 2,000 documents.
- TF-IDF representation with 8,000 features.
- The matrix has 16,000,000 possible entries and is **99.282% sparse**.
- K-Means clusters documents and displays representative terms for interpretation.

### Dimensionality reduction and comparisons
- Truncated SVD reduces the representation to 50 dimensions.
- The 50 components explain **11.99%** of the variance.
- External clustering comparison:

| Representation | ARI | NMI |
|---|---:|---:|
| Original TF-IDF | **0.3876** | **0.4958** |
| 50-dimensional Truncated SVD | 0.2865 | 0.4498 |

- On the SVD representation, K-Means (K=4) has silhouette 0.0746 with cluster sizes 212, 310, 379 and 1,099.
- A diagonal-covariance GMM (K=4) has silhouette −0.0341 with cluster sizes 232, 811, 350 and 607; it converges in 47 EM iterations.

The results show that dimensionality reduction is not automatically beneficial for every clustering metric. Here, the original TF-IDF representation has stronger ARI/NMI values than the tested 50-dimensional representation.

## Methods demonstrated
Exploratory data analysis, missing-value handling, standardisation, K-Means, Gaussian Mixture Models, AIC/BIC model selection, silhouette analysis, DBSCAN, density/noise sensitivity, TF-IDF, sparse matrices, Truncated SVD, ARI and NMI.


## NLP category copy
A complete byte-for-byte copy of this combined notebook is also available in [`05-NLP/`](../05-NLP/README.md), alongside copies of all three CSV dependencies. The canonical notebook remains here; the NLP copy is for convenient category navigation.
