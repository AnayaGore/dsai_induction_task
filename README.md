# README

## Name & Branch
- Anaya Gore
- CSE

## Model Architecture & Core Idea
- Task: multi-label classification of Wikipedia comments (toxic, severe_toxic, obscene, threat, insult, identity_hate); metric = mean column-wise ROC AUC
- Preprocessing: minimal; TF-IDF with sublinear term frequency and unicode accent stripping; no manual cleaning
- Features: word TF-IDF (1-2 grams, 100k features) + character TF-IDF (char_wb, 2-5 grams, 100k features), stacked side by side
- Model: logistic regression (liblinear), C = 2.0
- Multi-label setup: 6 independent binary classifiers, one per label; output = predicted probability per label
- Validation: 80/20 stratified hold-out (stratified on toxic), scored with mean ROC AUC
- Final model: refit on 100% of the training data, predicted on the test set
- Results: baseline 0.9766 -> char n-grams 0.9856 -> tuned C 0.9862 (validation); leaderboard 0.9870

## Unique / Differentiating Ideas
- Added character n-grams to handle misspelt and disguised swear words; largest gains on threat (+0.014) and identity_hate (+0.013)
- Tuned regularisation C over [1, 2, 4, 8]; best at C = 2, larger C overfit
- Found and fixed a column-order bug in the submission by comparing validation (0.986) with the first leaderboard score (0.94)

