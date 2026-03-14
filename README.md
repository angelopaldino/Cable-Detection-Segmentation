# Thin Cable Instance Segmentation & Line Fitting (TTPLA Dataset)
This repository contains the winning solution for a Computer Vision competition focused on the automated detection and geometric analysis of power lines and cables. The project addresses the challenging task of segmenting thin structures and estimating their mathematical line equations using the TTPLA (Transmission Tower and Power Line Architecture) dataset.

## Achievement
Metric achieved: LDS (Line Detection Score) = 2.9753
Performance: Outperformed the ResNet-50 baseline by significant margins in both mAP and topological consistency.

## Task
The goal of this project was twofold:Pixel-level Segmentation: Identify and segment individual pixels belonging to cables in complex outdoor aerial imagery.Geometric Estimation: Compute the mathematical equation of the line coinciding with the cable's skeleton (Polar Coordinates: $\rho$, $\theta$).

## Challenges
Thin Structures: Cables often occupy only a few pixels in width, leading to discontinuities in standard segmentation models.

Topological Preservation: Ensuring the connectivity of the predicted masks.

Geometric Precision: Accurate angle estimation is crucial for infrastructure monitoring.

## Proposed solution


Our approach utilizes the state-of-the-art Mask2Former architecture with strategic optimizations:
Model Architecture
Framework: Mask2Former (Masked-attention Mask Transformer).

Backbones: Evaluated ResNet-50, ResNet-101, and Swin-S (Transformer). The Swin-S backbone provided superior global context for long, thin structures.

Input Augmentation: Extended input from 3-channel RGB to 5-channel (RGB + X-coord + Y-coord) to provide spatial awareness.

Loss custom

 ## Geometric Line Detection (RANSAC + PCA)
 After generating segmentation masks, we implemented a robust extraction pipeline:Skeletonization: Reducing masks to single-pixel centerlines.RANSAC: Iterative line fitting to handle noisy predictions and outliers.SVD Refinement: Refining the $\rho$ and $\theta$ parameters for maximum precision.PCA Fallback: Principal Component Analysis is used as a fallback for high-confidence but complex segments.

 ## Hyperparameter Optimization
Utilized Optuna with TPE (Tree-structured Parzen Estimator) to fine-tune RANSAC thresholds, Canny sensitivity, and confidence scores to maximize the project-specific LDS metric.
