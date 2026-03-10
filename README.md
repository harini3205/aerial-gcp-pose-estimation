# Aerial GCP Pose Estimation

## Overview
This project implements a machine learning pipeline to detect Ground Control Point (GCP) markers in aerial drone images.

The model performs two tasks:
1. **Keypoint Localization** – Predict the pixel coordinates (x, y) of the GCP marker center.
2. **Shape Classification** – Classify the marker shape as:
   - Cross
   - Square
   - L-Shape

---

## Dataset
The dataset contains aerial drone images organized in a nested folder structure.

Example structure:

project_name/survey_name/gcp_id/image.JPG

The dataset contains:

- **train_dataset** – Images with annotations (`gcp_marks.json`)
- **test_dataset** – Images without annotations

Example label format:

{
  "image_path.JPG": {
    "mark": {
      "x": 1024.5,
      "y": 850.2
    },
    "verified_shape": "L-Shape"
  }
}

---

## Model Architecture
The model uses a **ResNet18 pretrained backbone** for feature extraction.

Two output heads are used:

- **Coordinate regression head** → predicts (x, y)
- **Shape classification head** → predicts marker shape

---

## Training Details

Images were resized to **224 × 224**.

Loss functions used:

- **MSELoss** for coordinate prediction
- **CrossEntropyLoss** for shape classification

Optimizer:

Adam optimizer with learning rate **0.0001**

---

## Data Handling
Some dataset entries did not contain the field **verified_shape**.

These samples were filtered before training.

---

## Output

The model generates a file called:

predictions.json

Example output format:

{
  "path/to/image.JPG": {
    "mark": {
      "x": 225.4,
      "y": 171.0
    },
    "verified_shape": "L-Shape"
  }
}

---

## Repository Files

SKYLARK.ipynb – notebook containing training and inference code  
predictions.json – predictions generated for the test dataset  
README.md – project documentation

---

## Model Weights

Due to GitHub file size limits, the trained model weights are hosted on Google Drive.

Download link:  
[Google Drive - Model Weights and Dataset](https://drive.google.com/drive/folders/1tkkghBjE8jXA2MbLgssmQ9jjc77CUvQK?usp=sharing)

## Author

Computer Vision Engineering Assignment  
Aerial GCP Pose Estimation
