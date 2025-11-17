# Supervised Wavelet-Based Event Detector Exploration
Neural Signal Processing • Machine Learning • Electrophysiology Analysis

This project implements a data-driven, interpretable, and largely unsupervised pipeline for classifying synaptic inhibitory postsynaptic currents (IPSCs) in patch-clamp electrophysiology data.

The goal:

Identify waveform features that distinguish true synaptic events from noise without relying on vision or manually created labels.

This project combines digital signal processing (DSP), wavelet decomposition, feature engineering, and machine learning to reveal meaningful structure in neural signals.

🔍 Overview of the Approach
1. Initial Peak Detection (Rule-Based)

Amplitude threshold (delta)

Slope threshold (slope_thresh)

Minimum inter-event distance (distance)

This produces candidate “events” from raw electrophysiology recordings.

2. Wavelet Decomposition (db4)

Each candidate waveform is decomposed into multiple frequency bands:

D1: highest-frequency detail

D2, D3: progressively smoother detail layers

A3: low-frequency approximation

Wavelet coefficients form the basis for all downstream features.

3. Feature Engineering

For each wavelet level (L0–L3), features include:

Energy

Standard deviation

Max/min

Kurtosis

Skewness

Zero-crossings

Entropy

Slope

Interaction features (e.g., L0_slope_by_energy, L3_energy_x_L3_min)

Elastic Net regression identifies the most informative subset.

4. Unsupervised Clustering

KMeans on a reduced feature space

Visualized using PCA

Cluster 1 consistently maps to true synaptic events

Achieved:

Precision: 0.806

Recall: 0.649

F1 score: 0.719

This significantly improves over the raw threshold detector (F1 = 0.49).

5. Supervised Sanity Checks

To validate that engineered features are informative:

Random Forest

SVM

Logistic Regression

SVM reached 0.77 accuracy on balanced labels.

📈 Key Results

Wavelet-based features capture biologically meaningful distinctions in IPSC shape.

Elastic Net highlights several powerful features:

L0_slope (sharpness)

L3_energy (structure of slower components)

L3_min (amplitude/polarity)

KMeans + feature engineering improves F1 score from 0.49 → 0.72.

Clear separability in PCA after proper feature selectio
