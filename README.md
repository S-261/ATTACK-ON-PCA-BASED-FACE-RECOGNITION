# Error In Zhang et al Facial Algorithm

## Overview

This document addresses issues related to Face Recognition as described by Zhang et al. In the provided Python implementation, we explore a crucial point where the client successfully computes the covariance matrix, using the following expression: $\( \mathbf{S} = \frac{1}{m}\mathbf{AA}^T \)$. Subsequently, Eigenvalue Decomposition (ED) is performed on encrypted version of $\mathbf{S}$ i.e. $\( \widetilde{\mathbf{U}} \)$. The existence of the ED of $\( \widetilde{\mathbf{U}} \)$ implies that the norm $\( \left\lVert \widetilde{\mathbf{U}} - \widetilde{\mathbf{Y}}\mathbf{\Lambda}\widetilde{\mathbf{Y}}^T \right\rVert \)$ should be negligible.

## Preprocessing

In the preprocessing step, we consider $\( \mathbf{A} \)$ as an image matrix with dimensions $\( 400 \times 170 \)$. The presence of a non-negligible value in the norm $\( \left\lVert \widetilde{\mathbf{U}} - \widetilde{\mathbf{Y}}\mathbf{\Lambda}\widetilde{\mathbf{Y}}^T \right\rVert \)$ serves as evidence, indicating inaccuracies in the decomposition due to issues in the encryption process.

## Symmetry Issue

A critical point is identified: the algorithm will not function correctly if the matrix $\( \widetilde{\mathbf{U}} \)$ (referred to as $\( \mathbf{U1} \)$ in the code) lacks symmetry.

## Solution

To address this issue, a workable fix is provided to ensure the functionality of the Zhang et al algorithm.

Feel free to refer to the provided Python code and documentation for a comprehensive understanding and implementation details.
