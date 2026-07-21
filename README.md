# Netflix Movies and TV Shows – EDA & Clustering (Machine Learning Project)

Exploratory data analysis and unsupervised clustering of Netflix's catalog for content segmentation, **"More like this"** recommendations, and strategy insights.

**Project Type:** EDA + Unsupervised Learning (Clustering)  
**Contribution:** Individual

---

## Overview

This repository contains two Jupyter notebooks that work with the **NETFLIX MOVIES AND TV SHOWS CLUSTERING** dataset:

1. **EDA notebook** – Explore and understand the catalog (distributions, trends, relationships).
2. **ML notebook** – Build clustering models (K-Means, Agglomerative) to group similar titles and support recommendations and content strategy.

The goal is to turn catalog data into **actionable segments** for similar-title recommendations, catalog balance, and acquisition decisions.

---

## Repository Structure

| File / folder                                | Description                                                                                                                                                   |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Sample_EDA_Submission_Template.ipynb`       | Exploratory Data Analysis: know your data, wrangling, 20+ visualizations (UBM), solution to business objective, conclusion.                                   |
| `Sample_ML_Submission_Template.ipynb`        | Machine Learning: same data + feature engineering, hypothesis tests, 15+ charts, K-Means & Agglomerative clustering with tuning, evaluation, save/load model. |
| `NETFLIX MOVIES AND TV SHOWS CLUSTERING.csv` | Dataset (7,787 titles): type, title, director, cast, country, date_added, release_year, rating, duration, listed_in (genres), description.                    |
| `netflix_kmeans_model.joblib`                | Saved best K-Means model (created when you run the ML notebook).                                                                                              |
| `netflix_scaler.joblib`                      | Saved StandardScaler (created when you run the ML notebook).                                                                                                  |
| `README.md`                                  | This file.                                                                                                                                                    |

---

## Dataset

- **Name:** NETFLIX MOVIES AND TV SHOWS CLUSTERING
- **Rows:** 7,787 titles (movies and TV shows)
- **Columns:** show_id, type, title, director, cast, country, date_added, release_year, rating, duration, listed_in, description

Missing values appear in director (~30%), cast (~9%), country (~6%), and smaller shares in date_added and rating; these are handled in the notebooks (e.g. filled with "Unknown" or medians where appropriate).

---

## EDA Notebook – What’s Inside

- **Know your data:** Load CSV, first view, shape, info, duplicates, missing-value count and bar chart.
- **Understanding variables:** Column list, describe, variable description table, unique-value counts.
- **Data wrangling:** Fill nulls (director, cast, country, rating), parse `date_added`, create `year_added`, `duration_min`, `duration_seasons`, `primary_genre`, `primary_country`.
- **Visualizations:** 20+ charts following **U**nivariate, **B**ivariate, **M**ultivariate (UBM) analysis. Each chart has: _Why this chart?_, _Insights_, _Business impact_.
- **Section 5 – Solution to Business Objective:** Concrete suggestions (catalog balance, geography, ratings, clustering readiness, trends).
- **Conclusion:** Summary of findings, business impact, and readiness for clustering.

---

## ML Notebook – What’s Inside

- **Know your data:** Same structure as EDA (import, load, first look, shape, info, duplicates, missing count + viz).
- **Data wrangling:** Same as EDA (duration parsing, primary genre/country, year_added, etc.).
- **Visualizations:** 15 charts with Why / Insight / Business impact.
- **Hypothesis testing:**
  - H1: Type vs Rating (chi-square).
  - H2: Release year by type – Movies vs TV Shows (Mann-Whitney U).
  - H3: Release year (binned) vs primary country (chi-square).
- **Feature engineering:**
  - Missing values: median fill for numeric; categorical nulls handled in wrangling.
  - Outliers: cap at 99th percentile for duration.
  - Categorical encoding: LabelEncoder for type, rating; top 15 genre/country, rest "Other"; then encoded.
  - Scaling: StandardScaler.
  - No train/test split (clustering on full catalog); imbalance N/A.
- **ML models:**
  - Model 1: K-Means base + elbow/silhouette, then tuning over k = 3–6.
  - Model 2: Agglomerative (ward/average/complete), tune k.
  - Model 3: K-Means with best k; comparison chart (silhouette by model).
- **Evaluation:** Silhouette score; business impact; choice of final model; model explainability (cluster profiles).
- **Save/load:** Best K-Means model and scaler saved with `joblib`; sanity check on unseen data.
- **Conclusion:** Wrangling, encoding, scaling, models, tuning, silhouette, deployment and next steps.

---

## Technologies & Libraries

- **Language:** Python 3
- **Notebooks:** Jupyter
- **Data:** pandas, numpy
- **Visualization:** matplotlib, seaborn
- **ML & preprocessing:** scikit-learn (StandardScaler, LabelEncoder, KMeans, AgglomerativeClustering, silhouette_score)
- **Statistics:** scipy (stats for chi-square, Mann-Whitney U)
- **Persistence:** joblib (save/load model and scaler)

---

## How to Run

1. **Clone or download** this repository and ensure `NETFLIX MOVIES AND TV SHOWS CLUSTERING.csv` is in the same directory as the notebooks.

2. **Install dependencies** (if needed):

   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn scipy joblib jupyter
   ```

3. **Run the notebooks** in order (EDA first, then ML):
   - Open `Sample_EDA_Submission_Template.ipynb` in Jupyter and run all cells (Kernel → Run All).
   - Open `Sample_ML_Submission_Template.ipynb` and run all cells.

   Or from the command line:

   ```bash
   jupyter nbconvert --execute --inplace Sample_EDA_Submission_Template.ipynb
   jupyter nbconvert --execute --inplace Sample_ML_Submission_Template.ipynb
   ```

4. After the ML notebook runs, `netflix_kmeans_model.joblib` and `netflix_scaler.joblib` will be created in the project folder.

---

## Business Impact

- **Content segmentation:** Clusters label groups of similar titles (e.g. "Recent US dramas," "International TV comedies") for strategy and merchandising.
- **Recommendations:** Same-cluster titles can power **"More like this"** and similar features.
- **Catalog & acquisition:** Insights on type, genre, country, and ratings support balance and regional/local content decisions.
- **EDA findings:** Movies dominate; catalog is skewed to recent years; TV-MA/TV-14 lead ratings; US, India, UK lead by count; International Movies, Dramas, Comedies are top genres.

---

## License

This project is for educational/portfolio use. The Netflix dataset is from a public source; check the dataset license for redistribution and usage terms.
