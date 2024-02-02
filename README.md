# Error In Zhang et al Facial Algorithm

## Overview

This document addresses issues related to Face Recognition as described by Zhang et al. In the provided Python implementation, we explore a crucial point where the client successfully computes the covariance matrix, using the following expression: $\( \mathbf{S} = \frac{1}{m}\mathbf{AA}^T \)$. Subsequently, Eigenvalue Decomposition (ED) is performed on encrypted version of $\mathbf{S}$ i.e. $\( \widetilde{\mathbf{U}} \)$. The existence of the ED of $\( \widetilde{\mathbf{U}} \)$ implies that the norm $\( \left\lVert \widetilde{\mathbf{U}} - \widetilde{\mathbf{Y}}\mathbf{\Lambda}\widetilde{\mathbf{Y}}^T \right\rVert \)$ should be negligible.

## Preprocessing

In the preprocessing step, we consider $\( \mathbf{A} \)$ as an image matrix with dimensions $\( 400 \times 170 \)$. The presence of a non-negligible value in the norm $\( \left\lVert \widetilde{\mathbf{U}} - \widetilde{\mathbf{Y}}\mathbf{\Lambda}\widetilde{\mathbf{Y}}^T \right\rVert \)$ serves as evidence, indicating inaccuracies in the decomposition due to issues in the encryption process.

## Symmetry Issue

A critical point is identified: the algorithm will not function correctly if the matrix $\( \widetilde{\mathbf{U}} \)$ (referred to as $\( \mathbf{U1} \)$ in the code) lacks symmetry.

## Solution

To address this issue, a workable fix is provided to ensure the functionality of the Zhang et al algorithm.

# Zhang et al. Face Recognition Protocol Vulnerability

## Introduction

Our investigation into Zhang et al.'s face recognition protocol revealed a critical vulnerability. We discovered that the distorted pair ($\widetilde{\mathbf{Y}'}$, $\mathbf{\Lambda}'$) successfully passed the verification process without detection. This attack had significant repercussions on the face recognition protocol, leading to incorrect outputs upon modifications. Notably, Zhang et al. did not mention or conduct experiments with any facial dataset.

To experimentally demonstrate our attack, we utilized the Celebrity Faces dataset from Kaggle, accessible [here](https://www.kaggle.com/code/jiaowoguanren/celebrity-face-image-dataset-tensorflow/input). After obtaining the Covariance matrix $\mathbf{S}$, we encrypted $\mathbf{S}$ using Zhang et al.'s protocol and computed the eigendecomposition of the encrypted matrix $\mathbf{U1}$ as explained in Section \ref{sec:algofix}.

## Experimental Validation

### Verification and Decryption

Assuming no manipulation by the cloud in the decomposition, correct decomposition passes the verification step. Subsequently, we perform decryption, followed by dimension reduction and testing the PCA algorithm.

### Testing with a Test Image $\mathbf{x}$

We use a test image $\mathbf{x}$ to validate the algorithm. In this instance, we selected an image of *Tom Hanks*, not included in our training image set used to construct $\mathbf{A}$. Applying the same transformations used to generate $\mathbf{W}$ from $\mathbf{A}$, we find the closest column vector for recognition.

### Alarming Results

After modifications, we detected *Tom Hanks*'s image being recognized as *Scarlett Johannson*. This underscores the efficacy of our proposed **CHEATING** method and highlights the ineffectiveness of Zhang et al.'s verification scheme.

## GitHub README Usage

Feel free to refer to the provided Python code and documentation for a detailed understanding of the attack, its implications, and the proposed solution.
