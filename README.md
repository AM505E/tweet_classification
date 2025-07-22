#  Disaster Tweet Classification

---

##  Project Overview

This project tackles a **binary text classification** task: determining whether a tweet is related to a disaster (`1`) or not (`0`).

###  Dataset
- Source: [Kaggle Disaster Tweets](https://www.kaggle.com/competitions/nlp-getting-started/)
- ~7,000 labeled tweets
- Key columns:
  - `text`: the tweet content
  - `target`: 1 (disaster), 0 (non-disaster)

###  Approach
1. Start with simple model Logistic Regression
2. Evaluate performance and compare
3. Implement and fine-tune a transformer-based model (RoBERTa)
4. Use precision, recall, and F1-score to evaluate due to class imbalance

---

##  Class Imbalance Observation

After removing duplicates:

- 57.4% of tweets are non-disaster
- 42.6% are disaster-related

This imbalance can skew accuracy-based evaluations. Therefore, F1-score is used for fairer performance assessment.

---

##  Text Preprocessing Pipeline

The text preprocessing step transforms raw tweet content into clean, model-ready input:

### 1. Normalization
- Adds space between lowercase and uppercase letters
- Converts text to lowercase
- Removes URLs, mentions (`@user`)

### 2. Special Character Handling
- Removes hashtag symbols (`#`) while keeping the word
- Removes punctuation and numbers
- Normalizes repeated characters (`soooo` → `so`, `heyyyy` → `hey`)

### 3. Token Processing
- Tokenizes text into individual words
- Removes English stopwords (e.g., "the", "and")

### 4. Lemmatization
- Reduces words to base form (`running` → `run`)

####  Observation:
- **Disaster tweets** tend to be **shorter**
- **Non-disaster tweets** are often **longer**
- Word count distribution is approximately normal

---

##  Models and Results

### 1.  Logistic Regression
- **Accuracy**: 82%
- **F1 Scores**:
  - Non-disaster: 0.86
  - Disaster: 0.77
- Grid Search improved stability but not overall accuracy

### 2.  Random Forest
- **Accuracy**: 78%
- Grid Search improved to 79%
- Underperformed compared to Logistic Regression

### 3.  RoBERTa (Pre-trained Transformer)
- Used `roberta-base` fine-tuned on the dataset
- **Accuracy**: 82%
- **F1 Scores**:
  - Non-disaster: 0.85
  - Disaster: 0.78

RoBERTa demonstrated more balanced performance and contextual understanding despite similar accuracy to Logistic Regression.

---

##  Summary

- Logistic Regression provided strong baseline performance.
- Random Forest underperformed and didn't generalize as well.
- RoBERTa showed superior balance and semantic understanding, with room for improvement through further fine-tuning.

---
