# Machine Learning — 2026W

A collection of applied machine learning notebooks covering supervised learning, unsupervised learning, and dimensionality reduction. Each notebook is self-contained with clean code, detailed markdown commentary, and reproducible results.

---

## Notebooks

| # | Notebook | Topics | Dataset |
|---|---|---|---|
| 1 | [Credit Card Default: EDA & Classification](01_credit_default_classification.ipynb) | EDA · sklearn Pipelines · Random Forest · KNN · GridSearchCV · ROC-AUC · Threshold Selection | UCI Credit Card Default (30K records) |
| 2 | [Electricity Demand Clustering](02_electricity_demand_clustering.ipynb) | Time-Series Feature Engineering · K-Means · Agglomerative Clustering · Elbow Method · Silhouette Score | UCI ElectricityLoadDiagrams 2011–2014 (370 clients) |
| 3 | [Dimensionality Reduction on MNIST](03_dimensionality_reduction_mnist.ipynb) | PCA · t-SNE · Locally Linear Embedding · Trustworthiness · Runtime Analysis | MNIST (70K images, 784 features) |
| 4 | [Decision Trees & Ensemble Methods](04_decision_trees_ensembles.ipynb) | Decision Trees · RandomizedSearchCV · Random Forest · AdaBoost · Extra Trees · Gradient Boosting · Learning Curves | UCI Credit Card Default (30K records) |

---

## Highlights

### Notebook 1 — Credit Card Default Classification
- Full scikit-learn `Pipeline` with `ColumnTransformer` (scaling, imputation, one-hot encoding) to prevent data leakage
- 5-fold stratified `GridSearchCV` for both Random Forest and KNN
- Youden's J threshold selection and its accuracy/recall trade-off — critical in imbalanced credit risk contexts
- **RF outperforms KNN** (ROC-AUC 0.758 vs 0.744)

### Notebook 2 — Electricity Demand Clustering
- Engineers average normalized hourly demand curves from 15-minute raw time series
- Optimal k selected by combining the elbow method with silhouette scores (k=4 for all-client, k=2 for single-client)
- **Single-client clustering recovers weekday/weekend behaviour** without ever seeing calendar labels
- Cluster 4 (4 anomalous clients) highlights the value of unsupervised methods for operational flagging

### Notebook 3 — Dimensionality Reduction on MNIST
- PCA (784 → 154 features, 95% variance retained) reduces features but **increases** RF training time — demonstrating that tree ensembles don't benefit from PCA the way linear models do
- t-SNE achieves near-perfect **trustworthiness (0.98)** and preserves digit clusters cleanly; LLE achieves 0.82 at ~35% lower runtime
- KNN on t-SNE 2D coordinates achieves 95.7% accuracy, nearly matching the full 784-feature RF baseline

### Notebook 4 — Decision Trees & Ensemble Methods
- Isolates the effect of `max_depth`, `min_samples_split`, and `criterion` on decision tree performance
- Demonstrates why `RandomizedSearchCV` (50 iterations, 250 fits) is preferred over `GridSearchCV` (1,440 combinations, 7,200 fits)
- Full ensemble benchmark: **Gradient Boosted Trees** achieves the highest F1; **Extra Trees** trains fastest
- Learning curves diagnose bias/variance and confirm all ensembles benefit from more data

---

## Tech Stack

```
Python 3.10
numpy · pandas · matplotlib · seaborn
scikit-learn (pipelines, preprocessing, model_selection, ensemble, manifold, decomposition)
```

---

## Setup

```bash
git clone https://github.com/willsuther/Machine-Learning-2026W.git
cd Machine-Learning-2026W
pip install numpy pandas matplotlib seaborn scikit-learn openpyxl
jupyter notebook
```

**External datasets** (not included in repo due to size):
- UCI Credit Card Default: [download here](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients) — or loaded automatically via URL in notebooks 1 & 4
- UCI ElectricityLoadDiagrams: [download here](https://archive.ics.uci.edu/ml/datasets/ElectricityLoadDiagrams20112014) — update `DATA_PATH` in notebook 2
- MNIST CSV: [download here](http://yann.lecun.com/exdb/mnist/) — update `DATA_PATH` in notebook 3

---

## Author

**Will Sutherland, MSc** — Applied Mathematics & Statistics, Acadia University  
[LinkedIn](https://linkedin.com/in/willsuther) · [GitHub](https://github.com/willsuther)
