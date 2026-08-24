# Pumpkinmeter: Personalized Movie Recommendations Using Spark

A collaborative-filtering movie recommendation engine built with Apache Spark MLlib, simulating a real-world deployment for a fictional streaming startup ("Ripe Pumpkins") evaluating whether personalized recommendations can improve user retention.

**[View the full project report (PDF/DOCX)](Report_Omprakash.docx)** · **[View the notebook (HTML)](https://htmlpreview.github.io/?https://github.com/nehaOmprakash/movie-recommendation-spark/blob/main/DataTranslation_Omprakash.html)** · **[View the notebook (Jupyter)](DataTranslation_Omprakash.ipynb)**

## Project Overview

**Business problem:** A startup movie-review platform wants to launch "Pumpkinmeter," a personalized recommendation score, to boost user engagement and retention. This project evaluates whether a Spark-based collaborative filtering model can generate reliable, business-relevant recommendations at scale.

**Goal:** Build and evaluate a collaborative filtering recommender using Apache Spark, then translate the technical output into actionable business insight for a non-technical audience (board-level presentation).

## Dataset

- **Source:** [MovieLens Latest Dataset](https://grouplens.org/datasets/movielens/) (GroupLens Research)
- **Scale:** 33M+ user ratings across thousands of movies
- **Fields used:**
  - `ratings.csv` — userId, movieId, rating (1–5), timestamp
  - `movies.csv` — movieId, title, genres

## Technical Approach

Built using **Apache Spark MLlib's Alternating Least Squares (ALS)** algorithm for collaborative filtering:

- Loaded and cached large RDD datasets from CSV for efficient reuse
- Tuned hyperparameters on a 50% data sample to manage memory constraints
- Trained the ALS model on the full 33M+ rating dataset
- Dynamically incorporated new user profiles (2 custom users, 10 ratings each) by unioning them into the training set and retraining
- Generated top-15 recommendations per user using `predictAll()`, filtered by minimum rating-count thresholds to simulate different confidence levels

## Results

Two custom users were tested under two filtering scenarios — recommendations restricted to movies with **≥25 ratings** (Scenario 1) vs. **≥100 ratings** (Scenario 2):

| | Scenario 1 (≥25 ratings) | Scenario 2 (≥100 ratings) |
|---|---|---|
| **User 1** | Niche, highly-rated titles (e.g., *Long Night's Journey Into Day*) | Established classics (e.g., *The Godfather Part II*, *Schindler's List*) |
| **User 2** | Niche titles (e.g., *Mushishi*, *Cosmos*) | Mainstream blockbusters (e.g., *The Lord of the Rings*, *Fight Club*) |

## Business Insight

Filtering thresholds directly trade off **personalization vs. confidence**:
- **Lower thresholds** surface more personalized, niche recommendations — but with less statistical confidence due to smaller sample sizes.
- **Higher thresholds** return well-known, broadly popular titles with higher reliability, but less individual nuance.

**Recommendation:** A hybrid strategy blending both thresholds can balance personalization with reliability — showing users a mix of confident, popular picks alongside more tailored, niche suggestions.

## Repo Contents

- `DataTranslation_Omprakash.ipynb` — full Spark/Python notebook (data loading, ALS training, evaluation)
- `DataTranslation_Omprakash.html` — rendered notebook output
- `Report_Omprakash.docx` — full written case report (methodology, results, business insights)
- `Presentation_Omprakash.pptx` — board-style presentation summarizing findings

## Tools Used

Apache Spark (MLlib, ALS), Python, Jupyter Notebook, RDDs/distributed computing

---
*Project completed as part of the M.S. Business Analytics program at Seattle University (Big Data Analysis coursework).*
