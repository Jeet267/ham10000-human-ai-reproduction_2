# HAM10000 Human-AI Reproduction Baseline

This repository contains the baseline code, models, and results for a human-AI collaboration reproduction study on the HAM10000 (Human Against Machine with 10000 training images) dataset. The dataset is used for dermatoscopic image classification.

## Contents

- **`notebook00920e0615.ipynb`**: Jupyter Notebook containing the data processing, model training, evaluation, and visualizations.
- **`metrics.json`**: Overall evaluation metrics of the model (accuracy, loss, etc.).
- **`per_class_metrics.csv`**: Detailed metrics broken down by skin lesion class (e.g., precision, recall, f1-score).
- **`history_fold0.csv`**: Training and validation loss/accuracy history across epochs.
- **`splits.csv`**: The train/validation/test splits used for the experiments.
- **Visualizations**:
  - `class_distribution_png.png`: Bar chart or plot showing the distribution of classes in the dataset.
  - `confusion_roc.png`: Confusion matrix and Receiver Operating Characteristic (ROC) curves.
  - `gradcam.png`: Grad-CAM visualizations explaining model predictions on sample images.
  - `learning_curves.png`: Training and validation loss/accuracy learning curves.
  - `reliability_baseline.png`: Reliability diagrams/calibration curves for the baseline model.

## Setup and Usage

1. Clone the repository:
   ```bash
   git clone https://github.com/Jeet267/ham10000-human-ai-reproduction_2.git
   ```
2. Run the `notebook00920e0615.ipynb` to reproduce the model training and evaluation results.
