# Sentiment Analysis on Nasi Lemak Burung Hantu Reviews

Classifying Google Reviews of **Nasi Lemak Burung Hantu**, a popular Klang Valley restaurant, as positive or negative, and finding the topics customers talk about most (food quality, service speed, pricing, cleanliness and ambience). Built in **RapidMiner (AI Studio)**.

## Objectives
1. Measure overall customer sentiment from historical Google Reviews
2. Identify the key themes in customer feedback
3. Give the owner data-driven recommendations to improve service and operations

## Data
- Scraped from Google Maps reviews with a browser data-scraping extension
- Split into **high** (4–5 stars, labelled positive) and **low** (1–3 stars, labelled negative) sets
- Non-English reviews translated into English (`Translated Review` column)
- Reviewer names removed before publishing

| File | Contents |
|---|---|
| `data/nlbh_high_reviews.csv` | 4–5 star reviews |
| `data/nlbh_low_reviews.csv` | 1–3 star reviews |
| `data/testing/nlbh_new_reviews_test.csv` | new unseen reviews for model testing |

## Method (RapidMiner process)
`rapidminer/nlbh_sentiment_training.rmp`
1. Label and append both sets, set `Sentiment` as the target
2. Text processing: transform cases → tokenize → remove English stopwords → filter by length → Porter stemming → n-grams
3. Feature selection: **Information Gain**, top **300** terms
4. Models: **Naive Bayes**, **SVM** and **Random Forest**
5. Validation: split validation (70/30, 80/20) and k-fold cross-validation (k = 5, 10)

`rapidminer/nlbh_model_testing.rmp` applies the trained model to new reviews using the same 300-term vocabulary.

## Results
| Model | Best accuracy |
|---|---|
| **Random Forest** | **76.35%** (70/30 split) |
| Naive Bayes | 75.49% (10-fold cross-validation) |
| SVM | 73.66% (10-fold cross-validation) |

All three models passed the 70% accuracy target, and Random Forest performed best.

## How to run
Open the `.rmp` files in RapidMiner / Altair AI Studio, then point the **Retrieve** operators at the CSV files in `data/`.

> Group project (4 members) for ISP610 Business Data Analysis, Bachelor of Information Systems (Hons.) Intelligent Systems Engineering, UiTM Shah Alam.
