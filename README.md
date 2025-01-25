# Nanoparticle Toxicity Analysis Pipeline

This repository contains a comprehensive Python-based pipeline for analyzing nanoparticle toxicity data. It includes various methodologies for data visualization, dimensionality reduction, and machine learning to uncover patterns and insights related to nanoparticle exposure and toxicity.

---

## Features

### 1. **Data Preprocessing**
- Summarizes cell counts based on well data.
- Normalizes data using Z-scores.
- Handles control wells (e.g., C03) separately for accurate comparisons.

### 2. **Visualization**
- **Heatmaps**: Generate heatmaps of cell counts across 96-well plates.
- **Histograms**: Analyze feature distributions using matplotlib and scipy.
- **Dimensionality Reduction**:
  - **PCA**: Principal Component Analysis for visualizing variance.
  - **UMAP**: Uniform Manifold Approximation and Projection for clustering.

### 3. **Machine Learning Models**
- **XGBoost**: Gradient boosting for toxicity prediction.
- **KNN**: K-Nearest Neighbors for classification.
- **MLP**: Multi-Layer Perceptron for deep learning-based analysis.

### 4. **Statistical Analysis**
- Performs LD50 extrapolation using a three-parameter logistic model.
- Handles cases where responses at the highest concentration do not drop below 50%.

### 5. **Customizable Code**
- Modular functions make it easy to extend or modify the pipeline for different datasets and analyses.

---

## Prerequisites

Before running the code, ensure you have the following installed:

- Python 3.9 or later
- Key Python libraries:
  - `numpy`
  - `pandas`
  - `matplotlib`
  - `seaborn`
  - `scipy`
  - `umap-learn`
  - `xgboost`
  - `sklearn`
