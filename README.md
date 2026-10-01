# Domain-Robust Deep Learning for Steel Microstructure Classification

A computer-vision study of **Bainite–Martensite microstructure classification** focused on model generalization across unseen physical specimens and microscopy acquisition conditions.

## Overview

High classification accuracy on randomly partitioned microscopy images does not necessarily imply reliable performance on unseen physical specimens. This project evaluates this gap using **5,293 microscopy images** and compares convolutional and transformer-based vision architectures under increasingly challenging validation settings.

The experimental pipeline evaluates:

- Custom CNN baseline
- ResNet18 transfer learning
- Vision Transformer (ViT-B/16)
- Swin Transformer (Swin-T)
- Physical-specimen-disjoint validation
- Microscope and magnification holdouts
- Grad-CAM interpretability
- Acquisition-aware augmentation
- Repeated grouped robustness validation

## Key Results

| Model | Standard Macro-F1 | Unseen-Specimen Macro-F1 |
|---|---:|---:|
| Custom CNN | 0.7789 | 0.6405 |
| ResNet18 | **0.9608** | 0.6702 |
| ViT-B/16 | 0.9404 | 0.7497 |
| Swin-T | 0.9236 | 0.7932 |
| Swin-T + Acquisition Augmentation | — | **0.8074** |

Despite achieving **0.9608 Macro-F1** under conventional evaluation, ResNet18 dropped to **0.6702** when tested on unseen physical specimens, demonstrating a substantial generalization gap.

Swin-T improved unseen-specimen Macro-F1 to **0.7932**, while acquisition-aware augmentation further increased performance to **0.8074**.

## Cross-Domain Evaluation

Generalization was explicitly evaluated across:

- unseen physical specimens
- 3 microscope configurations
- 3 magnifications (20x, 50x, 100x)

This allows model performance to be assessed beyond conventional random image-level train/test splitting.

## Experimental Pipeline

```text
Dataset Exploration
        ↓
Data Cleaning & Leakage-Safe Splitting
        ↓
Custom CNN Baseline
        ↓
ResNet18 Transfer Learning
        ↓
Cross-Domain Generalization
        ↓
Grad-CAM Failure Analysis
        ↓
ViT-B/16
        ↓
Swin Transformer
        ↓
Domain-Robust Training
        ↓
Repeated Specimen-Grouped Validation

├── notebooks/       # Experimental notebooks
├── results/         # Metrics, predictions and analysis outputs
├── literature/      # Literature used to motivate the study
├── report/          # Project report
├── src/             # Supporting source code
└── README.md