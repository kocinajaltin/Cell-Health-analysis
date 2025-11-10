# Nanoparticle Toxicity Analysis Pipeline

This repository contains a single Jupyter Notebook implementing a full workflow for analyzing nanoparticle toxicity using high-content imaging data. The notebook integrates data preprocessing, visualization, dimensionality reduction, and machine learning into one continuous analysis. Supplementary analyses (e.g., LD₅₀ estimation and some statistical summaries) were performed in Excel and are not part of the notebook code.

---

## Overview

The notebook processes cell-level data collected from 96-well plates to investigate the effects of different nanoparticles and concentrations on cellular morphology. It includes visual and statistical tools to explore exposure–response patterns.

---

## 1. Data Preprocessing and Quality Control

### **Plate-wise Heatmaps**

Generates 96-well heatmaps showing cell count distributions per plate.

**Generated in code:** `generate_heatmap()`

* Counts the number of cells per well.
* Displays plate uniformity and identifies abnormal wells (e.g., low counts, edge effects).

*Example outputs:*
![Plate 1 Heatmap](results/plate1_heatmap.png)
![Plate 2 Heatmap](results/plate2_heatmap.png)
![Plate 3 Heatmap](results/plate3_heatmap.png)

---

### **Coefficient of Variation (CV) Across Plates**

Calculates and visualizes variability across replicates.

* Computes mean, standard deviation, and coefficient of variation (CV) per well.
* Plots a heatmap of CV values across the 96-well format.

*Example output:*
![CV Heatmap](results/coefficient_variation_heatmap.png)

| Well | Mean | SD | CV    |
| ---- | ---- | -- | ----- |
| A01  | 204  | 16 | 0.078 |
| B01  | 190  | 14 | 0.074 |

---

## 2. Feature Distribution Analysis

### **Raw and Log-Transformed Histograms**

Visualizes distributions of quantitative imaging features (e.g., *Feature Area*) before and after log transformation.

**Generated in code:** `generate_combined_histograms_and_stats_with_cohen_d()`

* Creates histograms of raw and log-transformed data.
* Calculates descriptive statistics (mean, SD) and Cohen’s *d* for selected wells.
* Saves outputs as CSV files.

*Example outputs:*
![Raw Histogram](results/raw_histogram.png)
![Log Histogram](results/log_histogram.png)

**Output table:**

| Well | Mean (log) | SD (log) | Cohen’s *d* |
| ---- | ---------- | -------- | ----------- |
| B03  | 0.48       | 0.12     | 2.01        |
| D03  | 0.51       | 0.13     | 2.37        |

---

## 3. Dimensionality Reduction

### **Principal Component Analysis (PCA)**

Identifies features contributing to the largest variance in cell morphology.

* Uses `scikit-learn` PCA on standardized features.
* Visualizes pairplots colored by nanoparticle type or concentration.
* Displays loading heatmaps and variance plots.

*Example outputs:*
![PCA Pairplot](results/pca_pairplot.png)
![PCA Loadings](results/pca_loadings.png)

### **Uniform Manifold Approximation and Projection (UMAP)**

Projects multidimensional data into two dimensions for visualizing exposure clusters.

* Conducted both per plate and for combined data.
* Generates scatter plots for single and multiple nanoparticle types.

*Example outputs:*
![UMAP All Particles](results/umap_all_particles.png)
![UMAP CuO Single Particle](results/umap_cuo_single_particle.png)

---

## 4. Machine-Learning Models

Implements classification models to distinguish control vs treated samples using cell morphology features.

### **Models in Code**

| Model   | Description                                          | Metrics                                  |
| ------- | ---------------------------------------------------- | ---------------------------------------- |
| XGBoost | Gradient boosting classifier for toxicity prediction | Accuracy, Precision, Recall, F1, ROC-AUC |
| KNN     | K-Nearest Neighbors for label-based classification   | Accuracy, ROC-AUC                        |

Each model outputs confusion matrices, feature importance plots, and performance summaries.

*Example outputs:*
![Confusion Matrix Example](results/confusion_matrix_dose.png)
![Feature Importance](results/feature_importance_dose.png)

**Supplementary:** Deep learning (MLP) and LD₅₀ modeling were explored in Excel and are not included in the Jupyter code.

---

## 5. Supplementary Analyses (Excel)

Some calculations and curve fittings (e.g., LD₅₀ extrapolation, logistic modeling, and advanced statistics) were performed outside Python using Excel.
Results from these analyses complement the notebook outputs but are not executable within the Jupyter environment.

![LD50 Curve Example](results/ld50_curve.png)

---

## 6. Running the Notebook

The workflow is contained in a single Jupyter Notebook file. Run each section sequentially to reproduce the full analysis.

```bash
jupyter notebook nanoparticle_analysis.ipynb
```

---

## 7. Dependencies

Requires **Python 3.9+** and the following packages:

```
numpy
pandas
matplotlib
seaborn
scipy
scikit-learn
xgboost
umap-learn
tqdm
```

Install dependencies via:

```bash
pip install -r requirements.txt
```

---

## 8. Outputs Summary

| Analysis                 | Output Type                 | Example File                              |
| ------------------------ | --------------------------- | ----------------------------------------- |
| Heatmaps                 | PNG                         | results/plate*_heatmap.png                |
| Coefficient of Variation | PNG                         | results/coefficient_variation_heatmap.png |
| PCA                      | Pairplots, loadings         | results/pca_*                             |
| UMAP                     | 2D projections              | results/umap_*                            |
| Machine Learning         | Metrics, confusion matrices | results/model_*                           |
| Supplementary (Excel)    | LD₅₀ curves, summaries      | results/excel_outputs/*                   |

---

## 9. Citation

If you use this notebook or its derived analyses, please cite this repository and acknowledge the nanoparticle toxicity analysis workflow.
