# ECGCNN-SE: Squeeze-and-Excitation Enhanced Dual-Input CNN for Atrial Fibrillation Detection

This repository contains the PyTorch implementation of a modified deep learning architecture for detecting Atrial Fibrillation (AF) using ECG signals. The model builds upon the [ECG_DualNet repository by Rohr et al. (2022)](https://github.com/ChristophReich1996/ECG_Classification), with improvements based on Squeeze-and-Excitation (SE) blocks and model evaluation on the MIT-BIH Atrial Fibrillation Database (AFDB).


## Overview

The project explores the integration of SE blocks into a dual-branch architecture that processes:
- Time-domain ECG signals using an LSTM encoder.
- Frequency-domain spectrograms using a residual CNN encoder conditioned by the latent vector from the LSTM.


## Modifications from Original Work

- Added **Squeeze-and-Excitation (SE)** blocks to each spectrogram encoder residual block.
- Enhanced feature recalibration to improve AF detection sensitivity.
- Trained and evaluated on MIT-BIH AFDB dataset with 33,403 Normal and 22,781 AF segments.
- Model configurations: `ECGCNN_L` (baseline) vs. `ECGCNN_SE` (SE-enabled).

---

## Model Training Performance (100 Epochs)

| Validation Metric| ECGCNN_L | ECGCNN_SE |
|------------------|----------|-----------|
| Accuracy         | 93.00%   | 93.60%    |
| F1 Score         | 64.88%   | 76.05%    |
| Loss             | 0.4992   | 0.4691    |

Training graphs for loss, accuracy, and F1 score per epoch are included in the `figures/` folder.

---

## Repository Contents

- `Main_Implementation.ipynb` – End-to-end Jupyter notebook for training and evaluation
- `Inference.ipynb` – Notebook to test inference on unseen ECG inputs
- `config.py` – Hyperparameters and architecture configuration (modified from Rohr et al.)
- `train.py` – Training script for ECGCNN_L and ECGCNN_SE (modified from Rohr et al.)
- `model.py` – Core model file containing the ECGCNN architecture with SE block (modified from Rohr et al.)
- `__init__.py` – Marks the directory as a Python package (modified from Rohr et al.)
- `SE_training_outcomes.zip` – Includes training metrics and saved weights for ECGCNN_SE
- `L_Training_outcomes.zip` – Training results and logs for ECGCNN_L baseline
- `figures/` – Plots of validation loss, accuracy, and F1 score and test confusion matrices for AFDB dataset

## Setup Instructions

To recreate the reported performance or train the models from scratch:

1. Clone the original repository by Rohr et al.:

<pre> ```bash git clone https://github.com/ChristophReich1996/ECG_Classification.git
cd ECG_Classification ```
</pre>

2. Replace the following files in the cloned repo with the modified versions from this project:
- `train.py`
- `config.py`
- `model.py`
- `__init__.py`

3. Open and run `Main_Implementation.ipynb` to train either the ECGCNN_L or ECGCNN_SE model from scratch using the [Physionet/CinC 2017 Challenge Dataset](https://studtudarmstadtde-my.sharepoint.com/personal/christoph_reich_stud_tu-darmstadt_de/_layouts/15/onedrive.aspx?id=%2Fpersonal%2Fchristoph%5Freich%5Fstud%5Ftu%2Ddarmstadt%5Fde%2FDocuments%2FUni%2FECG%5FClassification%2Fdata%2Ezip&parent=%2Fpersonal%2Fchristoph%5Freich%5Fstud%5Ftu%2Ddarmstadt%5Fde%2FDocuments%2FUni%2FECG%5FClassification&ga=1).

To only run inference:

1. Follow steps 1–2 above to replace the required files.
2. Open `Inference.ipynb` and aet the path to your test ECG data.
3. Load the corresponding trained model from `SE_training_outcomes.zip` or `L_Training_outcomes.zip`.
4. Run inference and view predicted AF classifications.
