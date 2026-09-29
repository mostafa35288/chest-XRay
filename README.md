# 🩻 Chest X-Ray Pneumonia Detection

A Deep Learning project for detecting pneumonia from chest X-ray images using Artificial Neural Networks (ANN), Convolutional Neural Networks (CNN), and Transfer Learning with MobileNetV2.

The project compares different deep learning approaches and evaluates their performance using classification metrics and confusion matrices.

---

## 📌 Project Overview

Pneumonia detection from chest X-ray images is a binary image classification problem where each X-ray is classified as:

- `NORMAL`
- `PNEUMONIA`

In this project, three different approaches were implemented and compared:

1. Artificial Neural Network (ANN)
2. Convolutional Neural Network (CNN)
3. Transfer Learning using MobileNetV2

The project also includes a Gradio interface that allows users to upload a chest X-ray image and receive a prediction.

---

## 🎯 Objectives

- Analyze and preprocess chest X-ray images.
- Build an ANN-based binary classifier.
- Build a CNN specifically designed for image classification.
- Apply Transfer Learning using MobileNetV2.
- Compare the performance of the different models.
- Evaluate models using accuracy, precision, recall, F1-score, and confusion matrices.
- Build a simple interactive interface for X-ray prediction.

---

## 📊 Dataset

The project uses the **Chest X-Ray Pneumonia** dataset from Kaggle:

`paultimothymooney/chest-xray-pneumonia`

The training data contains two classes:

| Class | Training Images |
|---|---:|
| NORMAL | 1,341 |
| PNEUMONIA | 3,875 |
| **Total** | **5,216** |

The dataset is imbalanced, with more pneumonia images than normal images.

---

## 🔄 Data Preprocessing

The following preprocessing steps were applied:

1. Load X-ray images using OpenCV.
2. Resize images to `128 × 128`.
3. Convert images to grayscale.
4. Normalize pixel values to the range `[0, 1]`.
5. Encode labels:
   - `NORMAL → 0`
   - `PNEUMONIA → 1`

After preprocessing:

```text
X shape = (5216, 128, 128)
y shape = (5216,)
