# **Brain Tumor Segmentation Using Improved ResUNet++ Architecture**

> 🚀 **A powerful deep learning model for precise brain tumor segmentation in MRI scans using an enhanced ResUNet++ architecture, outperforming 3D models with a lightweight 2D approach.**

---

This project introduces an improved **ResUNet++ architecture** for **brain tumor segmentation** from multimodal MRI scans. The task is decomposed into **three binary 2D segmentation problems**—Whole Tumor (WT), Tumor Core (TC), and Enhancing Tumor (ET)—enabling high precision with reduced computational overhead. The architecture integrates **residual blocks**, **Squeeze-and-Excite modules**, **attention mechanisms**, and **Atrous Spatial Pyramid Pooling (ASPP)** to effectively capture multi-scale contextual information. Trained on the **BraTS 2020** dataset, the model achieves impressive **Dice Scores**: **0.9492 (WT)**, **0.9299 (TC)**, and **0.8895 (ET)**, outperforming many existing 3D models in both segmentation accuracy and robustness.
