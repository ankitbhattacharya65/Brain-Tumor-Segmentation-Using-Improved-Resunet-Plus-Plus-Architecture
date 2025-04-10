# **Brain Tumor Segmentation Using Improved ResUNet++ Architecture**

> 🚀 **A powerful deep learning model for precise brain tumor segmentation in MRI scans using an enhanced ResUNet++ architecture, outperforming 3D models with a lightweight 2D approach.**

---

This project introduces an improved **ResUNet++ architecture** for **brain tumor segmentation** from multimodal MRI scans. The task is decomposed into **three binary 2D segmentation problems**—Whole Tumor (WT), Tumor Core (TC), and Enhancing Tumor (ET)—enabling high precision with reduced computational overhead. The architecture integrates **residual blocks**, **Squeeze-and-Excite modules**, **attention mechanisms**, and **Atrous Spatial Pyramid Pooling (ASPP)** to effectively capture multi-scale contextual information. Trained on the **BraTS 2020** dataset, the model achieves impressive **Dice Scores**: **0.9492 (WT)**, **0.9299 (TC)**, and **0.8895 (ET)**, outperforming many existing 3D models in both segmentation accuracy and robustness.
## 📚 Dataset

This project utilizes the **BraTS 2020 (Brain Tumor Segmentation Challenge)** dataset, a gold standard for evaluating brain tumor segmentation algorithms in multimodal MRI scans. The dataset consists of pre-operative scans of glioblastoma and lower-grade glioma patients, with expert-annotated segmentation masks.

### 🔸 Dataset Details:
- **Total Training Cases:** 369
- **Image Dimensions:** 240 × 240 × 155 (Height × Width × Depth)
- **Pixel Value Range:** 0 – 255
- **Format:** NIfTI (.nii)

Each subject includes **five NIfTI files**:
- **Four MRI Modalities** (Channels):
  - 🧠 **T1** – Native T1-weighted
  - 💉 **T1CE** – Post-contrast T1-weighted with gadolinium enhancement
  - 🌊 **T2** – T2-weighted
  - 🧪 **FLAIR** – T2 Fluid Attenuated Inversion Recovery

- **One Segmentation Mask**, with pixel-wise labels:
  - `0` – Background
  - `1` – Necrotic and Non-Enhancing Tumor Core (NCR/NET)
  - `2` – Peritumoral Edema (ED)
  - `4` – GD-Enhancing Tumor (ET)

> ⚠️ Label `3` is not used (no pixels contain this label).

Each label contributes to the formation of three main binary segmentation tasks:
- **Whole Tumor (WT)** = Label 1 + 2 + 4
- **Tumor Core (TC)** = Label 1 + 4
- **Enhancing Tumor (ET)** = Label 4

> 📥 The dataset can be downloaded from the official BraTS 2020 challenge page:  
> [https://www.med.upenn.edu/cbica/brats2020/data.html](https://www.med.upenn.edu/cbica/brats2020/data.html)

