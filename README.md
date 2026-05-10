# Radar & AI for Hand Gesture Recognition
**Authors:** Pauline De Baets & Omar Ben Omar

**Date:** October 2025

This repository contains the final project for the course.
The project focuses on **automatic hand gesture classification** using radar micro-Doppler signatures and machine learning.

The goal was to build and compare different feature extraction and classification pipelines for recognizing hand gestures from radar spectrogram data.

## Project Overview

Radar-based gesture recognition is a promising approach for human–computer interaction because it can detect motion without requiring cameras or physical contact.

In this project, we classify four different hand gestures performed by multiple participants. The input data consists of radar spectrograms, which represent the time-frequency behavior of the gestures.

Two feature extraction methods were implemented and compared:

1. **Chebyshev Moments**
   - Based on the Cadence Velocity Diagram (CVD)
   - Converts radar spectrograms into compact 231-dimensional feature vectors
   - Tested with k-NN, SVM, and 1D CNN classifiers

2. **Micro-Doppler Signature Envelopes**
   - Extracts upper and lower frequency envelopes from the spectrogram
   - Uses empirically chosen threshold values
   - Tested with k-NN, SVM, and Logistic Regression classifiers

## Methods

### 1. Chebyshev Moments Pipeline

The Chebyshev method extracts features from the Cadence Velocity Diagram of each gesture.  
The main steps are:

- Load complex-valued spectrogram matrices
- Compute the modulus of the spectrogram
- Generate the Cadence Velocity Diagram using FFT along the time axis
- Resize the CVD images to a common shape
- Compute Chebyshev moments up to order 20
- Build a 231-dimensional feature vector
- Normalize the features using z-score standardization
- Train and evaluate different classifiers

The classifiers tested were:

- k-Nearest Neighbors
- Quadratic Support Vector Machine
- 1D Convolutional Neural Network

### 2. Micro-Doppler Signature Envelope Pipeline

The micro-Doppler envelope method extracts upper and lower frequency envelopes from the spectrogram.

The main steps are:

- Convert the spectrogram data to NumPy arrays
- Replace NaN values using column means
- Split the spectrogram into positive and negative frequency halves
- Compute upper and lower energy thresholds
- Extract significant frequency components
- Concatenate the upper and lower envelopes into one feature vector
- Train and evaluate different classifiers

The classifiers tested were:

- k-Nearest Neighbors
- Support Vector Machine
- Logistic Regression

## Results

The Chebyshev moment method performed significantly better than the micro-Doppler envelope method.

| Feature Extraction Method | Classifier | Best Accuracy |
|---|---:|---:|
| Chebyshev Moments | k-NN | 88.65% |
| Chebyshev Moments | 1D CNN | 86.31% |
| Chebyshev Moments | Quadratic SVM | 83.05% |
| Micro-Doppler Envelopes | k-NN | 67.0% |
| Micro-Doppler Envelopes | Linear SVM | 65.1% |
| Micro-Doppler Envelopes | Logistic Regression | 65.1% |

The best overall performance was achieved using **Chebyshev moments with a k-NN classifier**, reaching an accuracy of **88.65%**.


