# Predicting Nanoparticle Toxicity from High-Content Imaging Profiles

This repository presents a reproducible Jupyter Notebook for analyzing nanoparticle toxicity using high-content imaging data. The workflow integrates data preprocessing, visualization, dimensionality reduction, and machine learning to identify exposure–response relationships across nanoparticles and concentrations. Supplementary analyses (e.g., LD₅₀ modeling) were conducted in Excel.

![Workflow Overview](results/workflow_overview.png)

---

## Summary

Nanoparticles can induce diverse cellular responses that depend on particle type, size, and concentration. To characterize these effects, we applied a quantitative imaging-based approach inspired by morphological profiling studies such as the Broad Institute’s *Cell Health* project. The notebook processes plate-level data, normalizes features, and applies computational methods to reveal concentration-dependent patterns of toxicity.

---

## Pipeline Overview

The workflow comprises five main stages:

| Stage                       | Description                                                                                       | Output                             |
| --------------------------- | ------------------------------------------------------------------------------------------------- | ---------------------------------- |
| 1. Preprocessing            | Load, clean, and normalize well-level data using Z-scores; merge plates and handle control wells. | Cleaned datasets, summary tables   |
| 2. Visualization            | Generate heatmaps of well cell counts and histograms of key features.                             | PNG images                         |
| 3. Dimensionality Reduction | Apply PCA and UMAP to visualize sample clustering by nanoparticle and concentration.              | 2D projections, loading plots      |
| 4. Machine Learning         | Train XGBoost and KNN models to classify exposures and predict toxicity outcomes.                 | Model metrics, feature importances |
| 5. Supplementary Analyses   | Conduct LD₅₀ and curve-fitting calculations in Excel for concentration–response interpretation.   | Excel summaries, plots             |

---

## Data Preprocessing

The preprocessing module cleans and normalizes raw well data.

* Aggregates single-cell counts into well-level summaries.
* Identifies and removes outliers or missing values.
* Applies Z-score normalization using control wells.
* Merges multiple plate datasets for unified analysis.

*Example outputs:*
![Plate Heatmap](results/plate_heatmap.png)
![Control Comparison](results/control_distribution.png)

---

## Visualization and Feature Distributions

Feature distributions are examined using histograms of raw and log-transformed data. Statistical comparisons between wells are performed using Cohen’s *d* and descriptive metrics.

| Well | Mean (log) | SD (log) | Cohen’s *d* |
| ---- | ---------- | -------- | ----------- |
| B03  | 0.48       | 0.12     | 2.01        |
| D03  | 0.51       | 0.13     | 2.37        |

*Example outputs:*
![Histogram Raw](results/raw_histogram.png)
![Histogram Log](results/log_histogram.png)

---

## Dimensionality Reduction

Principal Component Analysis (PCA) and Uniform Manifold Approximation and Projection (UMAP) are used to capture feature variance and visualize cellular responses across nanoparticle types.

**PCA Summary:**

| PC | Individual Var (%) | Cumulative Var (%) |
| -- | ------------------ | ------------------ |
| 1  | 42.5               | 42.5               |
| 2  | 21.3               | 63.8               |
| 3  | 14.2               | 78.0               |

*Example outputs:*
![PCA Plot](results/pca_pairplot.png)
![UMAP Projection](results/umap_all_particles.png)

---

## Machine Learning

Machine-learning models predict nanoparticle-induced toxicity based on imaging features. The notebook implements XGBoost and KNN classifiers to distinguish control and exposed samples.

| Model   | Purpose                                                   | Key Metrics                              |
| ------- | --------------------------------------------------------- | ---------------------------------------- |
| XGBoost | Gradient boosting classifier for toxicity prediction      | Accuracy, Precision, Recall, F1, ROC-AUC |
| KNN     | Nearest neighbor classification for small-sample analysis | Accuracy, ROC-AUC                        |

*Example outputs:*
![Confusion Matrix](results/confusion_matrix.png)
![Feature Importance](results/feature_importance.png)

---

## Supplementary Analyses

Some analyses, including logistic curve fitting and LD₅₀ estimation, were performed in Excel to validate dose–response relationships.

![LD50 Curve](results/ld50_curve.png)

---


### Requirements

```
numpy
pandas
scipy
matplotlib
seaborn
scikit-learn
xgboost
umap-learn
tqdm
jupyter
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Citation

If you use this workflow, please cite this repository and acknowledge the nanoparticle toxicity analysis methodology based on high-content imaging data.
