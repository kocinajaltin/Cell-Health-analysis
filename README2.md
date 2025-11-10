# Nanoparticle Toxicity Analysis Pipeline

A Python-based workflow for analyzing nanoparticle toxicity using high-content imaging data. It includes automated data preprocessing, visualization, dimensionality reduction, and machine-learning models to explore cell-level responses across nanoparticles and concentrations.

---

## Repository Structure

```
├── data/                   # Raw and processed cell-level data
├── scripts/                # Analysis scripts
│   ├── preprocessing/      # Heatmaps, CV calculations, Z-score normalization
│   ├── dimensionality/     # PCA and UMAP analyses
│   ├── ml_models/          # XGBoost, KNN, and MLP models
│   └── statistics/         # LD50 and feature variance analysis
├── results/                # Figures and exported CSV summaries
├── notebooks/              # Exploratory notebooks (optional)
└── README.md               # Project documentation
```

---

## 1. Data Preprocessing and Quality Control

### **Plate-wise Heatmaps**

Generates 96-well heatmaps showing cell count distributions per plate.
*Example output:*

![Plate 1 Heatmap](results/plate1_heatmap.png)
![Plate 2 Heatmap](results/plate2_heatmap.png)
![Plate 3 Heatmap](results/plate3_heatmap.png)

**Function:** `generate_heatmap()`

* Annotates each well with cell counts.
* Highlights abnormal wells (e.g., edge effects or missing data).
* Optionally switches or corrects mislabeled wells.

---

### **Coefficient of Variation (CV) Across Plates**

Evaluates inter-plate reproducibility by computing mean, SD, and CV for each well.

| Well | Mean | SD  | CV    |
| ---- | ---- | --- | ----- |
| A01  | 204  | 16  | 0.078 |
| B01  | 190  | 14  | 0.074 |
| ...  | ...  | ... | ...   |

*Visualization placeholder:*
![CV Heatmap](results/coefficient_variation_heatmap.png)

---

## 2. Feature Distribution Analysis

### **Raw vs Log-Transformed Histograms**

Visualizes feature distributions (e.g., *Feature Area*) before and after log transformation.
Also computes descriptive statistics and Cohen’s *d* for selected wells.

**Output Table:**

| Well | Mean (log) | SD (log) | Cohen’s *d* |
| ---- | ---------- | -------- | ----------- |
| B03  | 0.48       | 0.12     | 2.01        |
| D03  | 0.51       | 0.13     | 2.37        |

**Figures:**

* ![Raw Histogram](results/raw_histogram.png)
* ![Log Histogram](results/log_histogram.png)

---

## 3. Dimensionality Reduction

### **Principal Component Analysis (PCA)**

Performs PCA to identify features driving cell morphology variance across nanoparticles or concentrations.

**Outputs:**

* Pairwise component plots (colored by particle or concentration)
  ![PCA Pairplot](results/pca_pairplot.png)
* Feature loadings heatmap
  ![PCA Loadings](results/pca_loadings.png)
* Explained-variance summary:

| PC | Individual Var (%) | Cumulative Var (%) |
| -- | ------------------ | ------------------ |
| 1  | 42.5               | 42.5               |
| 2  | 21.3               | 63.8               |
| 3  | 14.2               | 78.0               |
| 4  | 9.7                | 87.7               |
| 5  | 5.6                | 93.3               |

---

### **Uniform Manifold Approximation and Projection (UMAP)**

Embeds single-cell data into 2D space for visualizing exposure clusters.

**Scripts:**

* `prep_umap_data.py` → plate-specific UMAP embedding
* `umap_all_particles.py` → combined view of all nanoparticles
* `umap_single_particle.py` → concentration-series per particle

**Example outputs:**
![UMAP All Particles](results/umap_all_particles.png)
![UMAP CuO Single Particle](results/umap_cuo_single_particle.png)

---

## 4. Machine-Learning Models

### **Model Types**

| Model            | Purpose                                                             | Key Metrics                              |
| ---------------- | ------------------------------------------------------------------- | ---------------------------------------- |
| XGBoost          | Gradient boosting classifier for control vs compound discrimination | Accuracy, Precision, Recall, F1, ROC-AUC |
| KNN              | Distance-based classifier for small-sample validation               | Accuracy, ROC-AUC                        |
| MLP *(optional)* | Deep-learning model for nonlinear response mapping                  | Loss, Validation Accuracy                |

**Evaluation plots (per dosage):**

* Confusion matrices
  ![Confusion Matrix Example](results/confusion_matrix_dose.png)
* Feature importance bars
  ![Feature Importance](results/feature_importance_dose.png)
* Metric comparison charts
  ![Model Metrics](results/ml_metrics_plot.png)

---

## 5. Statistical Modeling

### **LD₅₀ Estimation**

Fits a three-parameter logistic regression to determine the concentration causing 50 % response reduction.
Handles plateauing curves when max response > 50 %.

![LD50 Curve Example](results/ld50_curve.png)

---

## 6. Example Workflow

```bash
# Preprocess and normalize raw well data

# Generate QC heatmaps and CV analysis

# Run PCA and UMAP for dimensionality reduction

# Train machine-learning classifiers

```

---

## 7. Dependencies

Requires **Python 3.9 +** and the following packages:

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

Install with:

```bash
pip install -r requirements.txt
```

---

## 8. Results Overview

| Analysis   | Output               | File                                        |
| ---------- | -------------------- | ------------------------------------------- |
| Heatmaps   | PNG                  | `results/plate*_heatmap.png`                |
| CV Heatmap | PNG                  | `results/coefficient_variation_heatmap.png` |
| PCA        | Pairplots + loadings | `results/pca_*`                             |
| UMAP       | 2D projections       | `results/umap_*`                            |
| ML metrics | JSON / CSV           | `results/model_metrics.csv`                 |

---

## 9. Citation

If you use this pipeline, please cite this repository and acknowledge the nanoparticle toxicity analysis workflow.
