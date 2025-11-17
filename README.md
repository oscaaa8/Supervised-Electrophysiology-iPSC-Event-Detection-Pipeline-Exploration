# Unsupervised Wavelet-Based Neural Event Detector  
### Neural Signal Processing • Machine Learning • Electrophysiology Analysis

This project implements a data-driven, interpretable, and largely unsupervised pipeline for classifying synaptic inhibitory postsynaptic currents (IPSCs) in patch-clamp electrophysiology data.

The goal is to identify waveform features that distinguish true synaptic events from noise without relying on vision or manually created labels.

This project combines digital signal processing (DSP), wavelet decomposition, feature engineering, and machine learning to reveal meaningful structure in neural signals.

---

## Overview of the Approach

### 1. Initial Peak Detection (Rule-Based)

Candidate peaks were selected from raw electrophysiology recordings using:
- Amplitude threshold (`delta`)
- Slope threshold (`slope_thresh`)
- Minimum inter-event distance (`distance`)

This produced a set of candidate “events” for further analysis.

---

### 2. Wavelet Decomposition (db4)

Each candidate waveform was decomposed into multiple frequency bands:

- D1: highest-frequency detail  
- D2/D3: progressively smoother detail layers  
- A3: low-frequency approximation  

Wavelet coefficients served as the foundation for downstream feature extraction.

---

### 3. Feature Engineering

For each wavelet level (L0–L3), the following features were computed:

- Energy  
- Standard deviation  
- Maximum and minimum  
- Kurtosis  
- Skewness  
- Zero-crossings  
- Entropy  
- Slope  

Additionally, several interaction features were engineered, such as:
- `L0_slope_by_energy`
- `L3_energy_x_L3_min`
- `L0_slope_minus_L1_std`

Elastic Net regression was used to identify the most informative subset of features.

---

### 4. Unsupervised Clustering

KMeans clustering was performed on the engineered feature space.

Visualization with PCA showed meaningful separation between event and non-event categories.

Cluster 1 consistently mapped to true synaptic events.

Performance metrics:
- Precision: 0.806  
- Recall: 0.649  
- F1 Score: 0.719  

This represents a significant improvement over the initial threshold detector (F1 = 0.49).

---

### 5. Supervised Sanity Checks

To validate that the engineered features were informative, several supervised models were tested:

- Random Forest  
- Support Vector Machine (SVM)  
- Logistic Regression  

The SVM model reached 0.77 accuracy on balanced labels, confirming that the feature set captured discriminative structure.

---

## Key Results

- Wavelet-based features captured biologically meaningful distinctions in IPSC waveform shape.
- Elastic Net identified several high-value features, including:
  - `L0_slope`  
  - `L3_energy`  
  - `L3_min`
- Feature engineering improved the KMeans F1 score from 0.49 to 0.72.
- PCA showed clear separation after feature selection.

---

## Documentation

The full project report is available in the repository:

