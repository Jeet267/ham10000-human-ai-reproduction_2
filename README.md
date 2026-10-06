# M2 — Human–Computer Collaboration for Skin Cancer Recognition (Baseline Reproduction)

This repository contains the baseline code, models, and results for a reproduction study of the paper:
**[Tschandl et al. (2020), *Human–computer collaboration for skin cancer recognition*]**

## 📖 Project Overview

The primary objective of this project is to build the foundational Machine Learning model described in the study's Methods section. 

* **Base Model:** ResNet34 (ImageNet-pretrained)
* **Dataset:** HAM10000 (Human Against Machine with 10000 training images), featuring 7 classes of skin lesions.
* **Goal:** Achieve comparable metrics to the paper on the ISIC 2018 test set:
  * **Target Mean Recall (Balanced Accuracy):** 77.7% (95% CI 70.3–85.1)
  * **Target Accuracy:** 80.3%

## 🔬 Methodology

### 1. Leak-Free Split (Crucial)
The HAM10000 dataset contains multiple photos of the same lesion (same `lesion_id`). A random split would leak data (same lesion in train and test), leading to artificially high accuracy (>90%). To prevent this, we use a strict `StratifiedGroupKFold` split:
* **Group:** `lesion_id`
* **Stratify:** class

### 2. Class Imbalance Handling
The dataset suffers from extreme class imbalance (e.g., Melanocytic nevi (NV) is ~67%, while Dermatofibroma (DF) is ~1%). Thus, pure accuracy is a misleading metric. The primary evaluation metrics utilized are **Mean Recall (Balanced Accuracy)** and **AUC**.

### 3. Training Config
Hyper-parameters strictly follow the paper's specifications with the addition of `EARLY_STOP_PATIENCE = 10` to prevent overfitting.

## 📂 Repository Contents

* **`notebook00920e0615.ipynb`**: The main Jupyter Notebook handling data loading, leak-free splitting, model training, evaluation, and visualizations.
* **`splits.csv`**: The exact train/validation/test splits used for the experiments.
* **`metrics.json`** & **`per_class_metrics.csv`**: Overall and per-class evaluation metrics (accuracy, precision, recall, f1-score, etc.).
* **`history_fold0.csv`**: Training and validation loss/accuracy history across epochs.
* **Visualizations**:
  * `class_distribution_png.png`: Bar chart demonstrating the class imbalance.
  * `confusion_roc.png`: Confusion matrix and Receiver Operating Characteristic (ROC) curves.
  * `gradcam.png`: Grad-CAM visualizations providing model interpretability on sample predictions.
  * `learning_curves.png`: Training and validation loss/accuracy learning curves.
  * `reliability_baseline.png`: Calibration curves (reliability diagrams) for the baseline model.

## 🚀 Setup & Usage (Kaggle)

This code is optimized to run seamlessly on Kaggle:

1. **Create New Notebook** → File → *Import Notebook* → Upload `notebook00920e0615.ipynb`.
2. Go to the Right panel → **Add Input** → Search for `skin-cancer-mnist-ham10000` (by *kmader*) → Add.
3. In **Settings**:
   * **Accelerator:** GPU T4 x2 (or P100).
   * **Internet:** On (Required to download ImageNet pre-trained weights).
4. Run all cells. (One fold takes ≈ 45–90 min).
   * *Tip: Use "Save Version → Save & Run All (Commit)" to run the execution in the background.*
