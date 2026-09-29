For CNN training, the images were reshaped to:

(5216, 128, 128, 1)

For Transfer Learning, grayscale images were converted back to RGB:

(5216, 128, 128, 3)
🧠 Models
1. Artificial Neural Network (ANN)

The ANN receives flattened 128 × 128 images.

Architecture
Input
  ↓
Dense(512, ReLU)
  ↓
Dropout(0.5)
  ↓
Dense(256, ReLU)
  ↓
Dropout(0.3)
  ↓
Dense(1, Sigmoid)

The images are flattened from:

128 × 128 = 16,384 features
Training
Optimizer: Adam
Loss: Binary Cross-Entropy
Batch Size: 32
Maximum Epochs: 20
Early Stopping: Enabled
2. Convolutional Neural Network (CNN)

A custom CNN was implemented to extract spatial features directly from the X-ray images.

Architecture
Input: 128 × 128 × 1
        ↓
Conv2D(32, 3×3, ReLU)
        ↓
MaxPooling2D
        ↓
Conv2D(64, 3×3, ReLU)
        ↓
MaxPooling2D
        ↓
Conv2D(128, 3×3, ReLU)
        ↓
MaxPooling2D
        ↓
Flatten
        ↓
Dense(128, ReLU)
        ↓
Dropout(0.5)
        ↓
Dense(1, Sigmoid)
Training
Optimizer: Adam
Loss: Binary Cross-Entropy
Batch Size: 32
Maximum Epochs: 20
Early Stopping: Enabled
3. Transfer Learning — MobileNetV2

MobileNetV2 pretrained on ImageNet was used as a feature extractor.

The original grayscale images were converted to RGB before being passed to MobileNetV2.

Architecture
Input: 128 × 128 × 3
        ↓
MobileNetV2 (ImageNet)
        ↓
GlobalAveragePooling2D
        ↓
Dense(128, ReLU)
        ↓
Dropout(0.5)
        ↓
Dense(1, Sigmoid)

The MobileNetV2 base model was frozen during training.

Training
Pretrained weights: ImageNet
Base model: Frozen
Optimizer: Adam
Loss: Binary Cross-Entropy
Batch Size: 32
Maximum Epochs: 20
Early Stopping: Enabled
📈 Results

The models were evaluated on a held-out test set containing 1,044 images.

Model	Accuracy	Macro F1-Score	Weighted F1-Score
ANN	90%	0.87	0.90
CNN	96%	0.95	0.96
MobileNetV2	90%	0.88	0.90

The custom CNN achieved the highest test accuracy among the implemented models.

🔍 Detailed Evaluation
ANN
              precision    recall  f1-score   support

NORMAL           0.80      0.81      0.80       268
PNEUMONIA        0.93      0.93      0.93       776

accuracy                             0.90      1044
macro avg        0.87      0.87      0.87      1044
weighted avg     0.90      0.90      0.90      1044
CNN
              precision    recall  f1-score   support

NORMAL           0.89      0.98      0.93       268
PNEUMONIA        0.99      0.96      0.97       776

accuracy                             0.96      1044
macro avg        0.94      0.97      0.95      1044
weighted avg     0.97      0.96      0.96      1044
MobileNetV2
              precision    recall  f1-score   support

NORMAL           0.75      0.91      0.82       268
PNEUMONIA        0.97      0.90      0.93       776

accuracy                             0.90      1044
macro avg        0.86      0.90      0.88      1044
weighted avg     0.91      0.90      0.90      1044
🧪 Prediction Example

The CNN model was also tested on an individual X-ray image.

Example output:

Prediction Probability: 0.9999975
Prediction: PNEUMONIA
🚀 Gradio Deployment

A simple Gradio interface was implemented to allow users to upload a chest X-ray image.

Workflow
Upload X-Ray
     ↓
Resize to 128×128
     ↓
Convert Grayscale → RGB
     ↓
Normalize
     ↓
MobileNetV2 Model
     ↓
Prediction Probability
     ↓
NORMAL / PNEUMONIA

The interface returns probabilities for both classes:

NORMAL
PNEUMONIA
🛠️ Technologies Used
Python
TensorFlow
Keras
OpenCV
NumPy
Pandas
Matplotlib
Seaborn
Scikit-learn
KaggleHub
Gradio
Deep Learning
Artificial Neural Networks
Convolutional Neural Networks
Transfer Learning
MobileNetV2
Image Classification
📂 Project Structure
chest-XRay/
│
├── chest_xray_مشسف.ipynb
│
└── README.md
⚙️ Installation

Clone the repository:

git clone https://github.com/mostafa35288/chest-XRay.git
cd chest-XRay

Install the required libraries:

pip install numpy pandas matplotlib seaborn tqdm tensorflow scikit-learn opencv-python kagglehub gradio
▶️ Running the Project

The project was developed as a Jupyter/Google Colab notebook.

Open:

chest_xray_مشسف.ipynb

Then run the notebook cells sequentially.

The notebook will:

Download the dataset.
Load and analyze the images.
Preprocess the images.
Train the ANN.
Train the CNN.
Train the MobileNetV2 transfer learning model.
Evaluate the models.
Launch the Gradio interface.
📌 Key Takeaways

This project demonstrates the difference between traditional fully connected neural networks and convolution-based architectures for image classification.

The experiments showed that the custom CNN achieved:

96% Test Accuracy

and provided stronger overall classification metrics than the ANN and MobileNetV2 models used in this project.

🔮 Future Improvements

Possible improvements include:

Data augmentation.
Handling class imbalance more explicitly.
Hyperparameter tuning.
Fine-tuning the pretrained MobileNetV2 layers.
Testing additional pretrained architectures.
Using larger image resolutions.
Adding explainability techniques such as Grad-CAM.
Deploying the model as a permanent web application.
Evaluating the model on external datasets.
⚠️ Disclaimer

This project is intended for educational and research purposes only.

It is not a medical diagnostic system and should not be used as a substitute for professional medical evaluation.

👨‍💻 Author

Mostafa Mohamed Zaki

GitHub:
https://github.com/mostafa35288

⭐ If you find this project useful, feel free to star the repository.
