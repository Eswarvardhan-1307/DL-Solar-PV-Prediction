# Sky-Image-Based Solar PV Power Forecasting

A two-stage deep learning project for short-term photovoltaic (PV) power forecasting using ground-based sky images from the **Stanford SKIPP'D 2019 dataset**.

The project first uses **SunNET**, a custom 2D CNN, to extract spatial features from individual sky images. These features are then passed to a **ConvLSTM–LSTM** network to learn cloud movement over time and predict future PV power.

## Project Overview

Cloud formation and movement can cause rapid changes in solar PV generation. This project uses sky images and their corresponding PV measurements to learn these visual and temporal patterns.

### Two-stage approach

1. **Stage 1 – SunNET (2D CNN):** Extracts spatial features from individual sky images. SunNET uses residual convolutional blocks with Squeeze-and-Excitation (SE) channel attention and CBAM spatial attention.
2. **Stage 2 – ConvLSTM–LSTM:** Uses sequences of SunNET feature maps to model the spatio-temporal evolution of clouds and generate a four-step-ahead PV forecast.

The complete forecasting setup uses six consecutive sky-image feature maps as input and predicts the next four PV values.

## Repository Structure

A suggested GitHub repository structure is:

```text
solar-pv-forecasting/
│
├── notebooks/
│   ├── BTP_stage1.ipynb
│   └── BTP_stage2_Final.ipynb
├── README.md
└── .gitignore
```

- `BTP_stage1.ipynb` – SunNET (2D CNN) training and feature extraction.
- `BTP_stage2_Final.ipynb` – Complete forecasting pipeline that uses SunNET outputs and the ConvLSTM–LSTM temporal model.
- `data/` – Local dataset directory. The raw dataset is downloaded separately and is not stored in this GitHub repository.

If your notebooks are in the repository's root directory instead of `notebooks/`, you can move them into that folder or update the paths in this README.

## Dataset

This project uses the **SKIPPD 2019 (Sky Images and Photovoltaic Power) dataset** for short-term solar PV power forecasting.

The dataset contains ground-based sky images and corresponding photovoltaic power measurements. This work uses the 2019 subset, consisting of 119,941 RGB sky images at a resolution of 64 × 64 pixels.

**Dataset source:** [SKIPPD 2019 – Kaggle](https://www.kaggle.com/datasets/eswarvardhankottana/skippd-dataset2019)

### Download Instructions

1. Visit the [SKIPPD 2019 Kaggle dataset page](https://www.kaggle.com/datasets/eswarvardhankottana/skippd-dataset2019).
2. Sign in to Kaggle and download the dataset (approximately 2 GB).
3. Extract the downloaded files into the project's `data/` directory.
4. Open the notebooks and update the dataset paths if your extracted folder structure is different.
5. Run the Stage 1 notebook before running the Stage 2 notebook.

## How to Run

1. Clone or download this repository.
2. Download and extract the dataset into `data/` by following the instructions above.
3. Install the Python libraries required by the notebooks. The notebooks contain the imports used by the project.
4. Run `notebooks/BTP_stage1.ipynb` to train SunNET and generate the spatial feature outputs.
5. Run `notebooks/BTP_stage2_Final.ipynb` to use the SunNET outputs and train/evaluate the complete ConvLSTM–LSTM forecasting model.

Run the notebooks in this order because Stage 2 depends on the feature outputs produced by Stage 1. Make sure the paths to the dataset, saved model, and generated feature files match your local environment.

## Technologies Used

- Python
- TensorFlow / Keras
- NumPy
- Matplotlib
- Jupyter Notebook
- Convolutional Neural Networks (2D CNN)
- Residual Learning and Attention Mechanisms (SE and CBAM)
- ConvLSTM and LSTM

## Notes

- Keep the raw dataset and large generated intermediate files out of GitHub unless you have a suitable external storage or data-hosting solution.
- If you change the folder locations, update the corresponding paths in both notebooks.
- The two notebooks should be run in sequence: Stage 1 first, then Stage 2.
