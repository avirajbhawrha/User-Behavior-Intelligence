# User Behavior Intelligence

Analyzing how people actually behave on a review platform , how they discover businesses, how they engage (reviews, tips, check-ins), and what separates a casual one-time reviewer from a highly engaged "elite" user — using the Yelp Open Dataset.

---

## 📌 Overview

Yelp connects millions of users to local businesses through ratings, written reviews, tips, and check-ins. This project digs into that behavioral data to answer a simple question: **what does user engagement actually look like, and what drives it?**

The project treats Yelp less like a review site and more like a behavioral dataset , using it to practice real-world data analytics skills: cleaning large semi-structured JSON data, engineering behavioral features, segmenting users, running sentiment analysis on review text, and connecting user behavior back to business performance.

## 🎯 Objectives

- **User Engagement Segmentation** — group users by activity level and value (RFM-style: Recency, Frequency, "usefulness" of reviews) to separate casual, regular, and power/elite users.
- **Business Performance Drivers** — identify which business attributes and categories correlate with higher ratings, review volume, and check-ins.
- **Sentiment vs. Star Rating** — check whether review *text* sentiment lines up with the *star rating* the same user gave, and flag mismatches.
- **Engagement Over Time** — track how review/tip/check-in activity trends by year, day of week, and season.
- **Elite User Behavior** — compare elite vs. non-elite users on review length, frequency, usefulness votes, and social graph (friends count).
- **(Stretch) Recommendation Foundation** — lay groundwork for a simple business recommender using user–business interaction patterns.

## 🗂️ Dataset

**Source:** [Yelp Dataset on Kaggle](https://www.kaggle.com/datasets/yelp-dataset/yelp-dataset)

The Yelp Open Dataset is a real (non-synthetic) subset of Yelp's businesses, reviews, and user data, released for academic and personal use, covering businesses across several metropolitan areas in the US and Canada. It ships as several newline-delimited JSON files:

| File | Description | Key Fields |
|---|---|---|
| `business.json` | Business listings | `business_id`, `name`, `address`, `city`, `state`, `postal_code`, `latitude`, `longitude`, `stars`, `review_count`, `is_open`, `attributes`, `categories`, `hours` |
| `review.json` | Full review text | `review_id`, `user_id`, `business_id`, `stars`, `text`, `date`, `useful`, `funny`, `cool` |
| `user.json` | User profiles & social graph | `user_id`, `name`, `review_count`, `yelping_since`, `friends`, `useful`, `funny`, `cool`, `fans`, `elite`, `average_stars` |
| `tip.json` | Short tips (shorter than reviews) | `text`, `date`, `compliment_count`, `business_id`, `user_id` |
| `checkin.json` | Check-in timestamps per business | `business_id`, `date` (list of timestamps) |
| `photo.json` *(optional)* | Photo metadata | `photo_id`, `business_id`, `caption`, `label` |

> **License note:** The dataset is distributed under Yelp's own Dataset Terms of Use — for personal/academic, non-commercial use only. See the [Kaggle page](https://www.kaggle.com/datasets/yelp-dataset/yelp-dataset) for the current license terms before any redistribution.

Given the dataset's size (several GB across files, millions of rows), this project works with a **sampled/filtered subset** (e.g., a handful of cities or a random sample of users/businesses) for local development, with an option to scale up.

## 🛠️ Tech Stack

- **Language:** Python 3.x
- **Data handling:** pandas, numpy, `json` (line-delimited JSON parsing)
- **Database (optional):** SQLite / PostgreSQL for querying at scale
- **Visualization:** matplotlib, seaborn, plotly
- **NLP / Sentiment:** NLTK / VADER or TextBlob
- **Modeling:** scikit-learn (clustering for segmentation, e.g., K-Means on RFM features)
- **Notebooks:** Jupyter

## 📁 Project Structure

```
User-Behavior-Intelligence/
├── data/
│   ├── raw/                  # Original Yelp JSON files (not committed — see .gitignore)
│   └── processed/            # Cleaned, filtered, and feature-engineered datasets
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_user_segmentation.ipynb
│   ├── 04_sentiment_analysis.ipynb
│   └── 05_business_performance.ipynb
├── src/
│   ├── data_loader.py        # Load & sample the large JSON files
│   ├── preprocessing.py      # Cleaning & feature engineering
│   ├── segmentation.py       # RFM / clustering logic
│   └── visualization.py      # Reusable plotting functions
├── reports/
│   └── figures/              # Exported charts for the writeup
├── requirements.txt
├── .gitignore
└── README.md
```

## 🔍 Methodology

1. **Data Ingestion** — stream-read the large newline-delimited JSON files, filter to a manageable subset (e.g., top N cities), and load into pandas/SQLite.
2. **Data Cleaning** — handle missing attributes, parse nested fields (`attributes`, `categories`, `hours`, `friends`), and normalize dates.
3. **Feature Engineering** — build per-user behavioral features: review recency, frequency, average stars given, useful/funny/cool votes received, elite status, tenure (`yelping_since`).
4. **User Segmentation** — apply RFM scoring and K-Means clustering to group users into behavioral segments (e.g., Power Users, Regulars, One-Timers, Dormant).
5. **Sentiment Analysis** — score review text sentiment and compare against the star rating to surface interesting mismatches.
6. **Business Performance Analysis** — link user segments back to business outcomes (ratings, review volume, check-in frequency) by category and location.
7. **Insights & Reporting** — summarize findings with visuals in `reports/`.

## ❓ Key Questions

- What separates an "elite" Yelp user from a regular one, behaviorally?
- Do users with more friends/fans write more useful reviews?
- Is there a mismatch between review sentiment and star rating, and does it vary by category?
- Which business categories see the highest review engagement (volume, usefulness)?
- How does user engagement trend over the years covered by the dataset?

## ▶️ How to Run

1. Download the dataset from [Kaggle](https://www.kaggle.com/datasets/yelp-dataset/yelp-dataset) and place the extracted JSON files in `data/raw/`.
2. Create a virtual environment and install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run the notebooks in `notebooks/` in numerical order, starting with `01_data_exploration.ipynb`.

## 📊 Results & Insights

_To be filled in as analysis progresses — segmentation profiles, sentiment-vs-rating findings, and business performance charts will be added here with supporting visuals from `reports/figures/`._


