# High-Content Imaging Analysis

## Overview
This repository contains Python scripts for analyzing high-content imaging data from 96-well plates. The analysis includes data preprocessing, visualization, and statistical computation for various particle exposures and concentrations. Key techniques include PCA (Principal Component Analysis), UMAP (Uniform Manifold Approximation and Projection), and heatmap generation for cell counts across wells.

---

## Features
1. **Batch Testing**:
   - Generates heatmaps of cell counts across wells for multiple plates.
   - Swaps and adjusts well counts as part of data curation.

2. **Coefficient of Variation (CV) Analysis**:
   - Calculates and visualizes the coefficient of variation across wells for each plate.

3. **Raw and Log-Transformed Data Visualization**:
   - Creates histograms and calculates Cohen's d for raw and log-transformed feature data.
   - Outputs descriptive statistics for specified wells.

4. **Z-Score Normalization**:
   - Implements normalization for data comparison across biological replicates.

5. **UMAP Analysis**:
   - Projects high-dimensional data to 2D space using UMAP.
   - Generates scatter plots for control wells and particles across concentrations.

6. **PCA Analysis**:
   - Performs PCA on selected features to reduce dimensionality.
   - Visualizes explained variance, cumulative variance, and PCA loadings.
   - Generates pair plots for visualizing principal components by particle type and concentration.

7. **PCA and UMAP Integration**:
   - Combines PCA and UMAP to analyze data from multiple plates and concentrations.

---

## Usage
### Prerequisites
- Python 3.7+
- Required libraries:
  - `numpy`
  - `pandas`
  - `matplotlib`
  - `seaborn`
  - `scikit-learn`
  - `umap-learn`
  - `tqdm`

