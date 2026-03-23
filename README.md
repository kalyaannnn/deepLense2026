# DeepLense GSoC 2026 — Results

---

## Common Test I. Multi-Class Classification

### Architecture

- **Models**: ResNet50, EfficientNet-B0, DenseNet121 (ImageNet pre-trained)
- **Training**: Cross-Entropy Loss, Adam optimizer
- **Dataset**: Normalized strong lensing images (3 classes)

### Results

| Model            | AUC-ROC |
|------------------|--------|
| DenseNet121      | 0.5092 |
| EfficientNet-B0  | 0.9859 |
| ResNet50         | 0.5093 |

### Visuals

<p align="center">
  <img src="figures/task1_efficientnet.pn" width="400"/>
  <img src="figures/task1_resnet.png" width="400"/>
</p>

---

## Specific Test IX. Foundation Model

### Task IX.A — Multi-Class Classification

#### Approach

- Self-supervised pre-training using **I-JEPA (ViT-S/8)** with 90% masking
- Fine-tuning with:
  - Attention pooling over patch tokens
  - Physics-Informed features (PINN)
  - Focal Loss + MixUp + Test-Time Augmentation

#### Results

- **Macro AUC**: **0.9691**

| Class          | AUC |
|----------------|-----|
| Axion          | 0.9688 |
| CDM            | 0.9438 |
| No Substructure| 0.9947 |

#### Visuals

<p align="center">
  <img src="figures/roc_curve.png" width="500"/>
</p>

---

### Task IX.B — Super-Resolution

#### Approach

- Fine-tuned encoder with **RCAN decoder**
- Residual learning + PixelShuffle upsampling
- Multi-loss training:
  - Charbonnier + SSIM + Frequency + Edge losses
- Physics-guided attention via deflection features

#### Results

| Metric | Value |
|--------|------|
| MSE    | **6.1×10⁻⁵** |
| PSNR   | **42.21 dB** |
| SSIM   | **0.9758** |

#### Visuals

<p align="center">
  <img src="figures/sr_results.png" width="700"/>
</p>

---

## Notes

- EfficientNet-B0 provides a strong baseline for classification.
- Physics-JEPA significantly improves structured substructure detection.
- Super-resolution results surpass bicubic baseline in all metrics.
