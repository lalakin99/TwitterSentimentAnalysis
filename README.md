#  Twitter Sentiment Analysis Project 

This project was completed by Stefano Gioda and Lal Akin for the lecture DSL of year 2021. 

## Project Overview
This repository contains the implementation and analysis of a **Twitter sentiment classification task**. The objective is to classify tweets as **positive (1)** or **negative (0)** sentiments using a variety of text embedding techniques and machine learning classification algorithms.

The main steps include:
1. **Preprocessing**: Cleaning and preparing the dataset.
2. **Text Embedding**: Applying methods like Bag of Words (BoW) and Term Frequency-Inverse Document Frequency (TF-IDF).
3. **Model Training and Evaluation**: Using Ridge Classifier, Linear Support Vector Classifier (SVC), and Random Forest Classifier.
4. **Hyperparameter Tuning**: Optimizing models with grid search for better performance.

---

## Problem Description
### **Data Overview**
- **Development Set**: Contains 224,994 rows, with 5 descriptive attributes and the sentiment column (used for training).
- **Evaluation Set**: Contains 74,999 rows, without the sentiment column (used for evaluation).

Attributes:
- `ids`: Unique numerical value for each tweet.
- `date`: Date and time of the tweet.
- `flag`: Query used to collect the tweet (constant value "NO QUERY").
- `user`: Username of the person who tweeted.
- `text`: The tweet content.

---

### **Preprocessing**
Steps taken to clean and prepare the dataset:
1. **Dropped Columns**:
   - `flag`: All values are constant and not informative.
   - `date`: Correlated with `ids`, so it was removed to avoid redundancy.
2. **One-Hot Encoding**: Applied to `user` for categorical conversion.
3. **Normalization**: Scaled `ids` using min-max normalization.
4. **Handling Text**:
   - Tokenization and lemmatization applied.
   - Stop words were retained as they improved model performance.
   - Duplicated `ids` with conflicting sentiments were dropped.

---

### **Text Embedding Techniques**
1. **Bag of Words (BoW)**:
   - Binary weighting scheme used to indicate word presence.
   - Results visualized with a word cloud.
2. **TF-IDF**:
   - Penalized redundant frequent words, handling stop words effectively.
   - Outperformed BoW in overall performance.
3. **n-Grams**:
   - Considered unigrams, bigrams, and trigrams during hyperparameter tuning.

---

### **Model Training and Evaluation**
Three classification models were evaluated:
1. **Ridge Classifier**:
   - Regularized regression-based model, ideal for high-dimensional data.
2. **Linear SVC**:
   - Fast and efficient support vector classification.
3. **Random Forest Classifier**:
   - Ensemble method using multiple decision trees (excluded from tuning due to lower performance).

---

### **Hyperparameter Tuning**
Grid search with 3-fold cross-validation was used to tune hyperparameters:
- **Preprocessing Parameters**:
  - n-Gram range: [(1,1), (1,2), (1,3)]
  - Minimum document frequency (`min_df`): [1, 2]
  - Binary weighting: [True, False]
- **Model-Specific Parameters**:
  - Ridge Classifier: `alpha` values [0.1, 1, 10].
  - Linear SVC: `C` values [0.1, 1, 10].

---

##  Results
After fine-tuning, the following F1 scores were achieved:
| Model            | Configuration       | F1 Score |
|-------------------|---------------------|----------|
| Ridge Classifier  | TF-IDF + User + IDs | 0.846    |
| Linear SVC        | TF-IDF + User + IDs | 0.845    |
| Baseline          | Leaderboard         | 0.753    |
