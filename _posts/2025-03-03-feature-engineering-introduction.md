---
layout: single
title: "feature engineering: the backbone of machine learning models"
date: 2025-03-03
categories: [Feature Engineering, Machine Learning, Feature Scaling]
tags: [Data Science, Feature Engineering, Machine Learning]
author_profile: true
read_time: true
comments: true
share: true
related: true
classes: wide
---

## What is Feature Engineering? 🔍

Feature engineering is the process of transforming raw data into meaningful features that enhance the performance of machine learning models. It involves selecting, modifying, or creating new variables (features) from the existing data to improve model accuracy.

But, before we dive into feature engineering, lets first understand what exatcly a feature is on context of machine learning.

## So what is a feature then?
​In machine learning, a feature is an individual measurable property or characteristic of a data sample that is used as input for a model generally denoted by `X`. Features serve as the foundational elements that algorithms utilize to identify patterns, make predictions, or classify data. ​


### There are widely two types of features, you will come across:


- *Numerical Features*: These are quantifiable attributes represented by numbers. Examples include age, height, weight, or income.​
<div >
    <p align="center" style="border: 1px solid #000">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/docs/feature-engineering-assets/numerical-features.png" alt="numerical-features" />
    <figcaption>numerical features.</figcaption>
    </p>
</div>



- *Categorical Features*: These are qualitative attributes that represent categories or groups, such as gender, color, or type of product.​ These features can be represented in numbers as well as strings.

<div >
    <p align="center" style="border: 1px solid #000">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/docs/feature-engineering-assets/categorical-features.png" alt="numerical-features" />
    <figcaption>categorical features.</figcaption>
    </p>
</div>

## How to deal with these features when training a machine learning model?

At first glance, data in machine learning might seem straightforward—just numbers ready for analysis. However, this assumption overlooks the complexities inherent in real-world data. Machine learning models function as mathematical functions, producing outputs based on given inputs. Consider a simple function like:

\[
f(x) = x + 3
\]

which computes an output for any valid \( x \).  

The challenge arises when the input data contains unexpected values, such as `NaN` (Not a Number) due to missing entries, or strings in place of numerical values. These anomalies can disrupt the model's computations, leading to errors or inaccurate predictions. Therefore, it's crucial to preprocess and transform data into formats that models can effectively interpret.  

This transformation process, known as **feature engineering**, involves creating new features or modifying existing ones to enhance model performance. Effective feature engineering can significantly improve a model's predictive accuracy by ensuring that the input data is both relevant and properly formatted.  

There are various techniques available for feature engineering, each addressing different data challenges. Common methods include:  

- **Creating interaction features** to capture complex relationships  
- **Feature Transformations** to transform some form of data into another form  
- **Feature Selection** to select only relevant features  
- **Feature Extraction** to extract only relevant features by combining two or more columns  
- **Handling missing values** through imputation  
- **Encoding categorical variables** into numerical formats  
- **Scaling features** to ensure uniformity  

Advanced techniques, such as **polynomial feature generation** and **target encoding**, further refine the feature set to optimize model performance.  

By thoughtfully applying these techniques, data scientists can transform raw data into a structured form that machine learning models can effectively utilize, leading to more accurate and reliable outcomes.  

<!-- Todo: Add chart -->





