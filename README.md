# LifeSpan
# Life Span Prediction from Long-term Historical Medical Notes

A Health Data Science project at [Insight Health Data Science](https://insightfellows.com/health-data) by Claire Hui Wu.


[Google Slides](https://docs.google.com/presentation/d/18Ph5_INtyxQMbcbIq_TOm40JN6EpjeSZi1HLGoyNUWs/edit?usp=sharing) * [Medium](https://medium.com/@chwu1811/lifespan-predict-life-span-based-on-long-term-medical-records-6bda5e3f1c47?sk=1789d7f732de41a999eec642ba69546d) * [LinkedIn](https://www.linkedin.com/in/clairehwu/)

- Summary: This project built a model to predict life span of patients with various diseases based on their medical notes.
- Keywords: Random Forest, Neural Newtork, TF-IDF, Word2vec 
- Libraries: sklearn, keras, tensorflow, LSTM, Matplotlib, NLTK, Spacy, pandas, numpy, wordcloud


---
## Table of content
- [Overview](#overview)
- [Pipeline](#pipeline)
- [Results](#results)

---

### Overview
Life Span has always been a critical factor for doctors to make treatment decisions. Many medical interventions have guidelines that suggest physicians take a patient’s prognostic life span into account. Most of the predictions today, however, are domain specific and inaccurate, which only look at the statistics of the survival rate for a certain disease without considering long-term and distinct medical conditions for each patient. In the meantime, physicians’ estimates of remaining life span are often inaccurate and overly optimistic. 

This project is dedicated to utilizing natural language processing techniques and machine learning models to predict prognostic life span based on patient medical records. The model aims to build an agnostic model that predicts lifespan for various diseases with low error and variance. 

---
### Pipeline

#### 1. Data exploration

The data comes with age and medical notes for each patient. The medical notes are from numerous different hospitals, scanned and then converted into one large text corpus. Therefore, all sorts of information, such as doctor visits, prescription medicine, fall incidents, patient identity, address, email correspondences, legal information are interwoven together, making this task even challenging.
<p align="center"> <img src="/Images/wordcloud.png" width="300" height="350">  </p>

#### 2. Preprocessing
 - Remove outliers. 
 
 The geriatric dataset is highly heterogeneous which contains medical notes longer than 2000 words, with age larger than 110 years, and remaining life span predictions larger then 250 months.  
 <p align="center"> <img src="/Images/data_cleaning.jpg" width="70%" height="70%"> </p>
 
 - Remove punctuation, unrecognized symbols and convert text to lowercase
 - Tokenization
 - Remove stop words, Stemming and Lemmatization 
 
 <p align="center"> <img src="/Images/nlp_pipeline.jpg" width="70%" height="70%"> </p>
 
#### 3. Text vectorization. 
 
 We apply two different techniques for vectorizing the text data. 
 
 1. TF-IDF 
 
 TF-IDF generated a 227k words vocabulary, which is quite a challenging for computing. A closer look at the frequency of the vocabulary, around 4000 words presented 99% of the total word frequencies. Taking the most frequent 4000 words, I converted the text medical notes to a 4000-dimension vector.
 
 2. Word2Vec
 
 We make use of the pretrained Word2Vec library Spacy to convert each word to a 300-dimension vector. To represent the entire notes for each patient, we simply apply element-wise addition to get a note level vector representation
 
#### 4. Model building and evaluation
  1. Evaluation metric
  
   R squared is a goodness-of-fit measure for regression models. It indicates the percentage of the variance in the target that are explained by the input values. R squared is intuitive since it measures the strength of the relationship between the model and target on a convenient 0–100% scale. The higher the better. 
  
  2. Models
  
  Life span is a complex problem which doesn't likely to be a linear relation between features and targets. In the meatime, the features in medical notes are highly correlated. These factors restricted us to models with less assumptions. Random Forest is a good model suits our problem with relative interpretability. In addition, we also included a Multilayer Perceptron model to better advance the model fitting and prediction. In reality, when interpretability to doctors outweights prediction precision, we can choose random forest, if vice versa, multilayer perceptron is a better choice. 
  
  3. Data Split
  
  Data were split into 70%/10%/20% for training/validation/testing.
  
  4. Model Prediction
  
  We trained on a random forest and multi-layer perceptron(MLP) on a train/val/test split with ratio 7:1:2. With a few hyperparameter tuning, random forest model gave 0.89 R-squared, which is pretty good. For MLP, we apply two dense layers each followed by one batch normalization layer and one dropout layer. It turns out that this regularization improved the R-squared even further to 0.93.

--- 
### Results

1. Random Forest R-squared and Feature Importances

<p align="center"> <img src="/Images/RF_r2.jpg" width="70%" height="70%">  </p>

2. Multilayer Perceptron R-squared and Mean Absolute Residual

<p align="center"> <img src="/Images/mlp.jpg" width="70%" height="70%">  </p>

