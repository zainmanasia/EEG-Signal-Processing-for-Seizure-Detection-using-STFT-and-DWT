# EEG Signal Processing for Seizure Detection using STFT and DWT

## Overview

Epilepsy is a neurological disorder characterized by abnormal, large-scale electrical activity in the brain. These dynamics can be captured using **electroencephalography (EEG)**, producing multi-channel time-series signals that reflect underlying neural activity.

This project explores **signal processing–based approaches** for automated seizure detection by analyzing EEG recordings in both the **time–frequency** and **multi-resolution** domains. Specifically, it evaluates the use of:

- **Short-Time Fourier Transform (STFT)** for localized spectral analysis  
- **Discrete Wavelet Transform (DWT)** using Haar wavelets for detecting abrupt changes in signal structure  

The goal is not to build a production-ready classifier, but to demonstrate how these transforms can extract meaningful features that correspond to seizure activity and serve as a foundation for downstream automated detection methods.

---

## Motivation

Clinical seizure detection often relies on manual inspection of EEG amplitude changes over time. While effective, this approach:
- Is labor-intensive
- Does not fully exploit the rich spectral structure of EEG signals
- Can struggle with non-stationary or transient patterns

Signal transforms such as STFT and DWT provide complementary perspectives:
- **STFT** reveals how frequency content evolves over time
- **DWT** captures transient, non-stationary features at multiple resolutions

Together, they offer a principled framework for identifying seizure-related dynamics beyond simple amplitude thresholds.

---

## Dataset

EEG recordings are sourced from publicly available datasets (e.g., UC Irvine Machine Learning Repository / Bonn EEG dataset), consisting of:

- Adult EEG recordings from epileptic and non-epileptic subjects
- Multi-channel time-series data
- Sampling rates on the order of ~170–256 Hz

Data is stored in **MATLAB `.mat` format** and loaded directly into the analysis pipeline.

---

## Methodology

### 1. Preprocessing
- EEG signals are reshaped and verified for consistency
- Basic visualization is performed to confirm signal validity
- Optional band-pass filtering may be applied depending on dataset characteristics

### 2. Short-Time Fourier Transform (STFT)
- EEG signals are segmented into overlapping windows
- STFT is applied to obtain a time–frequency representation
- Spectral power is analyzed to identify frequency-band activity associated with seizures

### 3. Discrete Wavelet Transform (DWT)
- Haar wavelets are used for multi-level 1-D decomposition
- Approximation and detail coefficients are extracted
- Detail coefficients highlight abrupt, transient changes in the signal

### 4. Feature Heuristics
- Band-limited spectral power from STFT
- Variance change-points derived from wavelet detail coefficients

These features are combined to produce **candidate seizure intervals**, which are compared against known seizure annotations where available.

---

## Results

The analysis demonstrates that:

- STFT effectively highlights seizure onset through increased power in characteristic frequency bands
- Haar DWT detail coefficients capture abrupt transitions associated with ictal activity
- Variance-based heuristics on wavelet coefficients provide a simple but effective indicator of seizure-related change points

Predicted seizure intervals show strong qualitative agreement with labeled seizure segments in the dataset.

---

## Notebook

A fully reproducible **Jupyter notebook** accompanies this project and implements the complete pipeline:

- Loading EEG data from `.mat` files
- STFT computation and visualization
- DWT decomposition and variance analysis
- Overlay of predicted seizure windows on EEG signals

The notebook also includes a **synthetic EEG fallback** for demonstration when real data is not available.

---

## Limitations

- The detection logic is heuristic and not clinically validated
- Results depend on dataset homogeneity and recording conditions
- No deep learning classifier is trained in this implementation

This work is intended as an **exploratory signal-processing study**, not a diagnostic tool.

---

## Future Work

Potential extensions include:
- Training CNN or hybrid CNN–wavelet models on extracted features
- Evaluating performance across broader EEG populations (pediatric, neonatal, animal models)
- Quantitative evaluation using sensitivity, specificity, and ROC-AUC
- Real-time seizure detection on streaming EEG data

---

## References

- Alotaiby et al., *EEG seizure detection using time-domain analysis*
- Mursalin et al., *Combined time–frequency feature extraction for seizure detection*
- Daubechies, *Ten Lectures on Wavelets*
- Bonn EEG Dataset, University of Bonn

---

## Acknowledgments

This project builds on foundational work in EEG signal processing and aims to provide an interpretable, method-driven baseline for seizure detection research.

