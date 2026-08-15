# Hybrid-Multimodal-Federated-Learning-for-Robust-Deepfake-Detection-under-Adversarial-Conditions
# README.md

# Hybrid Multimodal Federated Learning for Robust Deepfake Detection under Adversarial Conditions

A deepfake detection project developed during a research internship at **The LNM Institute of Information Technology (LNMIIT), Jaipur**, under the guidance of **Dr. Ashish Kumar Dwivedi**.

The project explores deepfake detection using **ResNet18** and combines **Federated Learning**, **FGSM adversarial training**, and **Coordinate-wise Median Aggregation** to improve the robustness of the detection system.

---

## Project Overview

Deepfake videos are synthetic or manipulated media generated using deep learning techniques. As deepfake technology becomes increasingly realistic, reliable detection has become important for cybersecurity, digital forensics, misinformation detection, and media authentication.

This project develops a deepfake detection pipeline using video-frame analysis and investigates a privacy-preserving Federated Learning setup with adversarial robustness mechanisms.

### Main Components

* **Celeb-DF v2** dataset
* Video frame extraction
* Image preprocessing
* **ResNet18** binary classifier
* **Federated Learning (FedAvg)**
* **FGSM adversarial attack generation**
* **Adversarial training**
* **Coordinate-wise Median Aggregation**
* Performance evaluation

---

## Objectives

The main objectives of the project are:

1. Develop a deep learning-based Real/Fake classifier.
2. Use ResNet18 for efficient image-based deepfake detection.
3. Implement Federated Learning using FedAvg.
4. Generate adversarial examples using FGSM.
5. Improve model robustness through adversarial training.
6. Apply coordinate-wise median aggregation to reduce the effect of abnormal or malicious client updates.
7. Evaluate and compare baseline, federated, and robust federated models.

---

## Methodology

```text
                 Celeb-DF v2
                      |
                      v
              Video Frame Extraction
                      |
                      v
             Image Preprocessing
                      |
                      v
                  ResNet18
                      |
                      v
              Local Client Training
                      |
                      v
              Federated Learning
                   (FedAvg)
                      |
                      v
          FGSM Adversarial Training
                      |
                      v
       Coordinate-wise Median Aggregation
                      |
                      v
                Global Model
                      |
                      v
                 Evaluation
```

---

## Dataset

The project uses the **Celeb-DF v2** deepfake dataset.

Dataset location used during development:

```text
/kaggle/input/datasets/reubensuju/celeb-df-v2
```

The dataset contains real and manipulated videos. Video frames were extracted and organized according to their labels.

### Classes

| Label | Class |
| ----- | ----- |
| 0     | Real  |
| 1     | Fake  |

The project primarily uses extracted frames for image-based classification.

---

## Technologies Used

### Programming Language

* Python

### Deep Learning

* PyTorch
* Torchvision
* ResNet18

### Computer Vision

* OpenCV
* FFmpeg

### Data Processing

* NumPy
* Pandas

### Machine Learning

* Scikit-learn

### Visualization

* Matplotlib

### Development Platform

* Kaggle Notebook

---

## Model Architecture

### ResNet18

ResNet18 was selected as the primary CNN architecture because of its relatively lightweight design and residual connections.

The original classification layer was adapted for binary classification:

```text
Input Image
    |
    v
ResNet18
    |
    v
Fully Connected Layer
    |
    v
Real / Fake
```

---

## Federated Learning

Federated Learning allows multiple clients to train a model locally without directly sharing their raw training data.

The implemented workflow is:

```text
             Global Model
                  |
        ---------------------
        |         |         |
        v         v         v
     Client 1  Client 2  Client 3
        |         |         |
        v         v         v
   Local Train Local Train Local Train
        |         |         |
        -------- Parameters --------
                  |
                  v
              Aggregation
                  |
                  v
             Global Model
```

The initial federated aggregation approach uses **Federated Averaging (FedAvg)**.

---

## FGSM Adversarial Training

The **Fast Gradient Sign Method (FGSM)** is used to generate adversarial examples.

The basic process is:

```text
Clean Image
     |
     v
Model Prediction
     |
     v
Calculate Loss
     |
     v
Calculate Input Gradient
     |
     v
Generate Perturbation
     |
     v
Adversarial Image
     |
     v
Adversarial Training
```

Adversarial training exposes the model to perturbed inputs so that it can learn more robust decision boundaries.

---

## Robust Aggregation

To reduce the influence of abnormal or potentially malicious client updates, **Coordinate-wise Median Aggregation** is used.

Instead of directly taking the mean of every client parameter, the median is calculated independently for each parameter.

```text
Client 1 Weights ----\
Client 2 Weights ----- > Coordinate-wise Median ---> Global Model
Client 3 Weights ----/
```

This approach is intended to provide greater robustness against outlier client updates.

---

## Project Workflow

### Week 1 – Dataset and Literature Study

* Studied deepfake detection
* Studied Celeb-DF
* Reviewed CNN-based detection
* Studied Federated Learning

### Week 2 – Dataset Preparation

* Loaded Celeb-DF v2
* Examined real videos
* Examined fake videos
* Extracted video frames

### Week 3 – Preprocessing

* Created frame datasets
* Assigned Real/Fake labels
* Prepared training, validation and testing data

### Week 4 – Model Development

* Implemented ResNet18
* Modified classification layer
* Started model training
* Addressed pretrained-weight download limitations in the initial offline Kaggle environment

### Week 5 – Federated Learning

* Created multiple simulated clients
* Implemented local training
* Implemented FedAvg
* Developed global model aggregation

### Week 6 – Evaluation

* Generated predictions
* Calculated Accuracy
* Calculated Precision
* Calculated Recall
* Calculated F1-score
* Generated evaluation plots

### Week 7 – Robust Defense

* Implemented FGSM adversarial examples
* Performed adversarial training
* Implemented coordinate-wise median aggregation
* Retrained the robust federated model
* Compared model performance

---

## Results

The following results were obtained during the project evaluation:

| Model                       | Accuracy (%) | Precision (%) | Recall (%) | F1 Score (%) |
| --------------------------- | -----------: | ------------: | ---------: | -----------: |
| Baseline ResNet18           |       100.00 |        100.00 |     100.00 |       100.00 |
| Federated Learning (FedAvg) |        66.15 |         66.15 |     100.00 |        79.63 |
| Robust FL (FGSM + Median)   |        66.15 |         66.15 |     100.00 |        79.63 |

> **Note:** These values represent the experimental results obtained in the project notebook and should be interpreted in the context of the particular dataset split, training configuration, and evaluation setup used.

---

## Evaluation Metrics

The project evaluates the models using:

* Accuracy
* Precision
* Recall
* F1 Score
* Confusion Matrix
* ROC Curve
* Training/validation loss
* Training/validation accuracy

These metrics provide a broader view of classification performance than accuracy alone.

---

## Project Structure

A recommended GitHub repository structure is:

```text
deepfake-detection-federated-learning/
│
├── README.md
│
├── notebooks/
│   ├── week1_dataset.ipynb
│   ├── week2_frame_extraction.ipynb
│   ├── week3_preprocessing.ipynb
│   ├── week4_resnet18.ipynb
│   ├── week5_federated_learning.ipynb
│   ├── week6_evaluation.ipynb
│   └── week7_robust_defense.ipynb
│
├── src/
│   ├── preprocessing.py
│   ├── model.py
│   ├── federated_learning.py
│   ├── adversarial_training.py
│   ├── aggregation.py
│   └── evaluation.py
│
├── results/
│   ├── confusion_matrix.png
│   ├── roc_curve.png
│   ├── accuracy_curve.png
│   ├── loss_curve.png
│   └── comparison.csv
│
├── figures/
│   ├── system_architecture.png
│   ├── federated_learning.png
│   └── fgsm_workflow.png
│
├── requirements.txt
│
└── LICENSE
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/deepfake-detection-federated-learning.git
cd deepfake-detection-federated-learning
```

Install the required packages:

```bash
pip install torch torchvision opencv-python numpy pandas matplotlib scikit-learn
```

For FFmpeg-based video processing, ensure FFmpeg is installed and available in the system path.

---

## Running the Project

The recommended workflow is:

```text
1. Prepare Dataset
       ↓
2. Extract Frames
       ↓
3. Preprocess Dataset
       ↓
4. Train ResNet18
       ↓
5. Run Federated Learning
       ↓
6. Generate FGSM Samples
       ↓
7. Perform Adversarial Training
       ↓
8. Apply Median Aggregation
       ↓
9. Evaluate Models
```

The notebooks can be executed sequentially according to the Week 1–7 workflow.

---

## Important Dataset Note

The Celeb-DF dataset is **not included in this repository** because of its size and dataset licensing/distribution considerations.

Download and configure the dataset separately, then update the dataset path in the notebooks.

---

## Limitations

The current implementation has several limitations:

* The federated clients are simulated rather than deployed across independent physical devices.
* The current implementation primarily uses video frames rather than a complete audio-video multimodal fusion pipeline.
* The reported results depend on the specific dataset split and experimental configuration.
* Differential privacy was considered as a future enhancement rather than being part of the final implemented defense pipeline.
* Real-time deployment was not implemented.

---

## Future Scope

Possible improvements include:

* Audio-video multimodal fusion
* Vision Transformer-based detection
* Larger and more diverse datasets
* Differential Privacy
* Secure model aggregation
* Byzantine-resilient Federated Learning
* Real-time deepfake detection
* Edge/mobile deployment
* Cross-dataset evaluation
* More extensive adversarial attack testing

---

## Internship Information

**Project:** Hybrid Multimodal Federated Learning for Robust Deepfake Detection under Adversarial Conditions

**Institute:** The LNM Institute of Information Technology (LNMIIT), Jaipur

**Guide:** Dr. Ashish Kumar Dwivedi

**Student:** Bhanu Pratap Singh Rathore

**Department:** Electronics and Communication Engineering

**College:** Poornima College of Engineering

**Training Period:** 2026

---

## Acknowledgement

I would like to express my sincere gratitude to **Dr. Ashish Kumar Dwivedi** for his guidance and support throughout the internship. I also thank **The LNM Institute of Information Technology (LNMIIT), Jaipur** and **Poornima College of Engineering** for providing the opportunity to work on this project.

---

## References

1. K. He, X. Zhang, S. Ren, and J. Sun, *Deep Residual Learning for Image Recognition*.
2. B. McMahan et al., *Communication-Efficient Learning of Deep Networks from Decentralized Data*.
3. I. J. Goodfellow et al., *Explaining and Harnessing Adversarial Examples*.
4. Y. Li et al., *Celeb-DF: A New Dataset for DeepFake Forensics*.
5. PyTorch and Torchvision documentation.
6. OpenCV documentation.
7. Scikit-learn documentation.

---

## Disclaimer

This repository contains work developed as part of an academic internship/research project. The implementation and reported results are intended for educational and research purposes.

---

## Author

**Bhanu Pratap Singh Rathore**

B.Tech – Electronics & Communication Engineering
Poornima College of Engineering
Internship at LNMIIT Jaipur
