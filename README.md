# Patch-DM with Gated Weight Blending

This repository explores improvements to patch-based diffusion models, specifically focusing on the **Patch-DM architecture**. The core novelty introduced here is a **Gated Weight Blender module** designed to improve structural coherence and smooth transitions between generated image patches.

---

## 🎥 Demo Video

Watch the project demo here:

[![Watch Demo]([https://www.youtube.com/watch?v=YOUR_VIDEO_ID](https://youtu.be/odP_rQNCaPQ))

---

## 📄 Project Report

Read the detailed report here:

👉 [Project Report]([https://your-report-link.com](https://drive.google.com/file/d/11aF39m1a-0tW82Zpb-10ULSA8ZXR4wx6/view?usp=sharing))

---

## 🚀 The Novelty: Gated Weight Blender

Standard patch-based models often struggle with **"seam" artifacts** where patches meet. Our implementation introduces a **learnable gating mechanism**:

- **Dynamic Blending**:  
  Instead of static averaging, a convolution-based gate calculates an alpha mask ($\alpha$) to weighted-blend original patches with spatially shifted neighbors.

- **Feature Awareness**:  
  The blender is integrated into the **UNet's final layers**, allowing the model to decide where to prioritize:
  - local patch detail  
  - global boundary smoothness  

---

## 📂 Repository Structure

The project is organized into two main streams:
- **Baseline (Standard Patch-DM)**
- **Novelty (Gated Weight Blender implementation)**

---

## 🧪 Micro-Experiments (100 Images)

Used for rapid prototyping and verifying architecture changes before full-scale training.

- `baseline_micro_7hr.ipynb`  
  Training the standard Patch-DM on a 100-image micro-dataset for 7 hours.

- `novelty_micro_7hr.ipynb`  
  Training the Gated Weight Blender version on the same micro-dataset.

- `baseline_micro_fid.ipynb` & `novelty_micro_fid.ipynb`  
  Scripts for generating reconstructions and calculating **FID scores** for the micro-scale tests.

---

## 🏛️ Full-Scale Experiments

Standard benchmarks for final performance comparison.

- `baseline_full_12hr.ipynb`  
  12-hour training run for the baseline model.

- `novelty_full_12hr.ipynb`  
  12-hour training run for the novelty model.

- `baseline_full_fid.ipynb` & `novelty_full_fid.ipynb`  
  Evaluation notebooks for generating high-fidelity reconstructions and calculating final **FID scores**.

---

## 🛠️ Core Utilities

- `latent-diffusion-model-training.ipynb`  
  General framework for training the latent embedding space and semantic encoder.

---

## ⚙️ Implementation Details

This project requires specific handling due to internal library constraints in the original Patch-DM codebase:

- **Monkey Patching**  
  Runtime monkey patching is used in evaluation notebooks to:
  - bypass Enum identity conflicts  
  - fix native `KeyError` bugs in the UCSD renderer  

- **Surgical Architecture Injection**  
  The novelty is injected into the **UNet at runtime**, ensuring:
  - compatibility with pretrained checkpoints  
  - correct weight mapping  

---

## 📊 Evaluation Methodology

To ensure a fair comparison, all models are evaluated using the **Fréchet Inception Distance (FID)**:

$$
FID = ||\mu_r - \mu_g||^2 + Tr(\Sigma_r + \Sigma_g - 2(\Sigma_r \Sigma_g)^{1/2})
$$

Where:
- $\mu_r, \Sigma_r$ → Mean and covariance of real images  
- $\mu_g, \Sigma_g$ → Mean and covariance of generated images  

👉 A **lower FID** indicates that generated images are closer to the real data distribution, demonstrating better model performance.

---

## 🏗️ Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/[Your-Username]/[Repo-Name].git
cd [Repo-Name]
```

### 2. Install Dependencies
```bash
pip install pytorch-lightning==1.9.5 lmdb==1.2.1 lpips pytorch-fid einops
```

### 3. Run Evaluation

Open any `_fid.ipynb` notebook to:
- load the corresponding checkpoint  
- generate reconstructions  
- calculate FID scores  

---

## 👩‍💻 Author

**Vandita Gupta**  
IIT Jodhpur
