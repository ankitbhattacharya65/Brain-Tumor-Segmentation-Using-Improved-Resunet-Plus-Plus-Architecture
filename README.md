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


## 🧪 Preprocessing

To reduce computational complexity, the original **3D MRI volumes** (240 × 240 × 155) from the BraTS 2020 dataset are converted into **2D slices**. Each subject contains 5 `.nii` files — 4 input channels and 1 ground truth segmentation mask. We excluded the **T1 (native)** modality due to its limited tumor contrast, retaining **T1CE, T2, and FLAIR** modalities.

### 🔹 Input Preprocessing:
- Extracted **10 representative 2D slices** per subject by fixing the slice index and iterating across the remaining dimensions.
- Each slice was resized to **128 × 128** pixels.
- **Normalization** was applied to each modality:  
  `Normalized = (pixel - mean) / std`
- Finally, the three channels (**T1CE, T2, FLAIR**) were **stacked** to form a single multi-channel 2D input.

### 🔹 Mask Preprocessing:
- Ground truth masks consist of:
  - `1` → Necrotic/Non-enhancing Tumor Core (NCR/NET)
  - `2` → Peritumoral Edema (ED)
  - `4` → Enhancing Tumor (ET)
  - `0` → Background
  - `3` → Not used (no pixels contain label 3)
- For **binary segmentation**, all non-zero labels were converted to `1` (tumor), preserving `0` for the background.
- Masks were reshaped to **2D slices (128 × 128)** in alignment with the image slices.

This preprocessing pipeline ensures the data is efficiently structured and normalized for optimal training of the 2D ResUNet++ architecture.
## 🧠 MRI Slices & Preprocessed Samples

### 📌 Fig 1: Showing a random slice of T1CE, T2, T2-FLAIR & Mask
![Fig 1](Fig 1-Showing a random slice of T1CE,T2,T2-FLAIR & mask.PNG)

### 🧪 Fig 2: Pre-processed images for Whole Tumor (WT)
![Fig 2](./Fig%202%20Pre-processed%20images%20For%20WT.png)

### 🧪 Fig 3: Pre-processed images for Tumor Core (TC)
![Fig 3](./Fig%203%20Pre-processed%20images%20For%20TC.png)

### 🧪 Fig 4: Pre-processed images for Enhancing Tumor (ET)
![Fig 4](./Fig%204%20Pre-processed%20images%20for%20ET.png)




