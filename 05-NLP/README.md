# 05 — Natural Language Processing (NLP)

## Dedicated notebook copy

`newsgroups-text-clustering (penguins.csv, airbnb_nyc.csv, newsgroups.csv).ipynb`

This is a byte-for-byte copy of the complete unsupervised-learning notebook also stored in `02-ML-Unsupervised/`. It is provided here so the NLP category contains an actual runnable notebook rather than only a README.

**Important scope note:** the source notebook is a combined three-practical assignment. The NLP work is its third practical (Newsgroups document clustering). The copied notebook therefore also contains the Penguin and NYC Airbnb clustering sections; those sections have not been removed or edited. The canonical notebook remains under `02-ML-Unsupervised/`.

## NLP implementation

The Newsgroups practical performs unsupervised document clustering:
1. Loads 2,000 text documents.
2. Converts documents into an 8,000-dimensional TF-IDF feature representation.
3. Inspects the sparse document-term matrix (99.282% sparsity).
4. Applies K-Means and inspects representative terms for each cluster.
5. Applies Truncated SVD to reduce the representation to 50 dimensions.
6. Compares clustering quality using Adjusted Rand Index (ARI) and Normalized Mutual Information (NMI).
7. Compares a further K-Means and diagonal-covariance GMM model on the reduced representation.

## Reported metrics

| Representation / model | ARI | NMI |
|---|---:|---:|
| Original TF-IDF + K-Means | **0.3876** | **0.4958** |
| 50D Truncated SVD + K-Means | 0.2865 | 0.4498 |

The 50 SVD components explain 11.99% of the variance. The 50D K-Means result has silhouette 0.0746; the diagonal GMM result has silhouette −0.0341 and converges in 47 EM iterations.

These results show that dimensionality reduction did not improve the reported external clustering metrics in this experiment. The labels used for ARI/NMI comparison are evaluation references, not supervised training targets.

## Dataset files

The copied notebook expects the following CSV files in its working directory:
- `newsgroups.csv` — required for the NLP practical.
- `penguins.csv` and `airbnb_nyc.csv` — required by the other two practicals retained in this complete notebook copy.

The three CSVs are available in `02-ML-Unsupervised/`. Copy them into this folder before running this duplicate notebook, or run the canonical notebook from its original folder. No dataset has been fabricated or substituted.

## Canonical source

[Canonical combined notebook](../02-ML-Unsupervised/clustering-lab%20(penguins.csv,%20airbnb_nyc.csv,%20newsgroups.csv).ipynb) · [Unsupervised ML README](../02-ML-Unsupervised/README.md)
