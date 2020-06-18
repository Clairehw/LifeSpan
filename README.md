# LifeSpan
# Life Span Prediction from Long-term Historical Medical Notes

A Health Data Science project at [Insight Health Data Science](https://insightfellows.com/health-data) by Claire Hui Wu.


[Google Slides]() * [Medium]() * [LinkedIn]() * [Resume]() * [Portfolio]()

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
Life Span has always been a critical factor for making clinical treatment decisions. Many medical interventions have guidelines that suggests physicians take a patient’s prognostic life span into account. Most of the predictions today, however, are domain specific and inaccurate, which only look at the statistics of survival rate for a certain disease without considering long-term and distinct medical conditions for each patient. In the meantime, physicians’ estimates of remaining life span are often inaccurate and overly optimistic. This project is dedicated to utilizing natural language processing techniques and machine learning models to predict prognostic life span based on patient medical records. The model aims to build an agnostic model that predicts lifespan for various diseases with low error and variance. 

---
### Pipeline

- Data exploratoration

We have age and medical notes for each patient. The medical notes are from numerous different hospitals, scanned and then converted into one large text corpus. Therefore, all sorts of information, such as doctor visits, prescription medicine, fall incidents, patient identity, address, email correspondences, legal information are interwoven together, making this task even challenging.
![GitHub Logo, 20%](/Images/wordcloud.png = 80x20)
- Preprocessing
 1. Remove outliers. We remove medical notes with age larger than 110 years, remaining life span predictions larger then 250 months, and medical notes with length larger than 2000 words.
 ![GitHub Logo](/Images/data_cleaning.jpg){height="70%" width="70%"}
 2. Remove punctuation, unrecognized symbols and convert text to lowercase
 3. Tokenization
 4. Remove stop words, Stemming and Lemmatization
 ![GitHub Logo](/Images/nlp_pipeline.jpg){:height="50%" width="50%"}
- Text vectorization. 
  
 We apply two different techniques for vectorizing the text data. 
 1. TF-IDF 
 TF-IDF generated a 227k words vocabulary, which is quite a challenging for computing. A closer look at the frequency of the vocabulary, around 4000 words presented 99% of the total word frequencies. Taking the most frequent 4000 words, I converted the text medical notes to a 4000-dimension vector.
 2. Word2Vec
- Model building and evaluation
  1. Evaluation metric
  
   R squared is a goodness-of-fit measure for regression models. It indicates the percentage of the variance in the target that are explained by the input values. R squared is intuitive since it measures the strength of the relationship between the model and target on a convenient 0–100% scale. The higher the better. 
  
  2. Model training



--- 
### Results
