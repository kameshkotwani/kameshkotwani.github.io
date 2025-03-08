---
layout: single
title: "🌱 Revolutionizing Cassava Disease Detection with Deep Learning"
date: 2024-09-03
description: "A deep learning model that classifies images using Convolutional Neural Networks."
categories: 
    - Machine Learning
    - Deep Learning
tags: [CNN,Deep Learning,Image Processing, mlflow,alexnet,imagenet,cassava,disease classification]

author_profile: true
related: true
read_time: true
header:
    teaser: assets/images/dissertation-teaser.webp
---
Cassava is a staple crop for millions, especially in **sub-Saharan Africa**, where it provides a crucial source of food and income. However, diseases such as **Cassava Mosaic Disease (CMD)** and **Cassava Bacterial Blight (CBB)** threaten yields, leading to severe food security challenges. Traditional disease detection relies on **manual inspection**, which is often **inaccurate, time-consuming, and not scalable**.

With advancements in **Deep Learning**, we can now automate disease detection using **Convolutional Neural Networks (CNNs)** trained on cassava leaf images. 🚀

---

## 🔍 The Aim of This Study

The goal was to **develop and evaluate CNN models** for detecting cassava leaf diseases using image-based classification. The research also compared different **CNN architectures, optimizers, and loss functions** to determine the best-performing model for accurate disease identification.

---

## 📊 Dataset & Methodology

A publicly available **Kaggle dataset** was used, consisting of **over 20,000 cassava leaf images**, labeled into:

- **Healthy Leaves**
- **Cassava Mosaic Disease (CMD)**
- **Cassava Brown Streak Disease (CBSD)**
- **Cassava Green Mottle (CGM)**
- **Cassava Bacterial Blight (CBB)**

### Key Steps in Model Development

---

#### 1. Data Preprocessing & Augmentation
  
- Images were resized to **227x227 pixels**  
- **Normalization** was applied to ensure consistent pixel values  
- **Augmentation techniques** (rotation, zooming, flipping) helped combat class imbalance  

#### 2. CNN Architecture & Model Training

- **Multiple CNN architectures** were tested  
- **Adam optimizer & RMSprop** were compared  
- **Loss functions:** *Categorical Cross-Entropy* vs *Focal Loss*  
- Hyperparameter tuning to improve accuracy  

#### 3. Evaluation Metrics

- **Accuracy, Precision, Recall, and F1-score** were used to evaluate model performance.  
- **MLflow** was used for **experiment tracking and parameter logging**.

---

## 🚀 Results & Key Findings

✅ **Best Model Achieved 93% Accuracy**  

- A **CNN model using Adam optimizer with Categorical Cross-Entropy loss** performed best.  
- The model successfully classified diseases, but **CMD was overrepresented**, indicating the need for more balanced datasets.

✅ **Adam Outperformed RMSprop**  

- Models trained with **Adam** converged faster and achieved better accuracy.

✅ **Focal Loss Did Not Outperform Categorical Cross-Entropy**  

- Contrary to expectations, **Focal Loss did not improve results**, highlighting the importance of dataset balancing techniques.

✅ **Overfitting Remained a Challenge**  

- Despite using **dropout layers and data augmentation**, the model tended to favor CMD due to dataset imbalance.

---

## 🔬 Future Work & Improvements

- **Hybrid Approaches:** Combining **CNN with XGBoost or Attention Mechanisms**.
- **More Data:** Expanding the dataset for better generalization.
- **Severity Assessment:** Extending the model to **predict disease severity** for better agricultural interventions.
- **Mobile App Deployment:** Enabling **real-time disease detection** for farmers using smartphones.

---

## 🌍 Why This Matters

This research **demonstrates the power of AI in agriculture**, paving the way for scalable, automated, and **cost-effective disease detection systems**. By leveraging deep learning, farmers and agronomists can **detect diseases early, improve yield, and combat food insecurity**.

## 📖 Read the full dissertation

[Disease Detection in Cassava Leaves using CNN]({{ site.url }}{{ site.baseurl }}/assets/docs/DissertationUniOfSheffieldCassavaLeaves.pdf)
