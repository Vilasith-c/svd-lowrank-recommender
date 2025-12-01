# Datasets and Reference Projects for SVD-Based Low-Rank Recommender

This document lists the main datasets and reference projects for your **“Low-Rank Matrix Factorization for Scalable Recommender Systems: An SVD-Based Approach”** project.  
For each item there is: a link and how you should use it in your project.

---

## 1. Datasets

### 1.1 MovieLens 100K (Primary Development Dataset)

- **Link (GroupLens official):**  
  https://grouplens.org/datasets/movielens/[web:19]  
- **Link (Kaggle mirror):**  
  https://www.kaggle.com/datasets/prajitdatta/movielens-100k-dataset[web:92]

**Usage in project (root idea):**

- Use as your **main dataset for development, debugging, and model tuning**.  
- Files include user–movie ratings (userId, movieId, rating, timestamp).  
- Steps:
  - Load into `data/` (e.g., `data/ml-100k/ratings.csv`).
  - Build the initial sparse user–item matrix \(R\).
  - Train and validate your **first SVD/MF model** here (quick training, easy iteration).
  - Use this dataset for **all core visualizations** and demos in the Streamlit app.

---

### 1.2 MovieLens 1M (Stronger Benchmark)

- **Link (GroupLens overview):**  
  https://grouplens.org/datasets/movielens/[web:19]  
- **Link (TFDS description):**  
  https://www.tensorflow.org/datasets/catalog/movielens[web:88]

**Usage in project:**

- Use as a **secondary dataset** to show that your approach scales beyond 100K ratings.  
- Train the same SVD/MF pipeline on 1M:
  - Compare **RMSE/MAE** vs 100K.
  - Measure **training time** and show a simple “time vs number of ratings” chart.
- Mention in project that “the same model design scales to 1M ratings” and back it with metrics.

---

### 1.3 MovieLens 20M / 25M (Optional Scalability Showcase)

- **Link (GroupLens 20M+):**  
  https://grouplens.org/datasets/movielens/[web:19]  

**Usage in project (optional but nice):**

- Use a **subset** (e.g., first 2–5M ratings) to:
  - Time SVD/MF training and **show scalability** of low-rank factorization.
  - Maybe compute only a small test RMSE on a validation split.
- This is mainly to support your “Scalable” in the title with **timing plots** and a short discussion.

---

### 1.4 Netflix Prize Data (Optional, Heavy)

- **Kaggle:**  
  https://www.kaggle.com/datasets/netflix-inc/netflix-prize-data[web:99]  
- **Academic Torrents:**  
  https://academictorrents.com/details/9b13183dc4d60676b773c9e2cd6de5e5542cee9a[web:93]

**Usage in project (only if needed):**

- Use **only for background / comparison mention**:
  - Describe that similar low-rank MF methods were used to compete in the Netflix Prize.
- Full training is probably too heavy for a student project, so you can:
  - Optionally sample a **small subset** to demonstrate that your code can handle the schema.
  - Mostly reference it in your README / presentation as related large-scale data.

---

## 2. Reference Projects (Matrix Factorization / Movie Recommenders)

### 2.1 MovieLens Matrix Factorization (Top‑K Recommender)

- **GitHub:**  
  https://github.com/MoMkhani/MovieLens-Matrix-Factorization[web:84]

**Usage in project:**

- Use as a **template for your MF backend**.
- Study:
  - How they load MovieLens and build the rating matrix.
  - Their matrix factorization loss and update rules (SGD/ALS).
  - Their `recommend_top_k` / similar helper functions.
- Adapt the structure into your `src/model_mf.py` and `src/recommend.py`.

---

### 2.2 Recommendation System Using Matrix Factorization

- **GitHub:**  
  https://github.com/SurhanZahid/Recommendation-System-Using-Matrix-Factorization[web:94]

**Usage in project:**

- Use as a **minimal, easy-to-understand code reference**.
- Good for:
  - Understanding MF from scratch: initializing user/item factor matrices, training loop, regularization.
  - Building a basic CLI or script that outputs recommendations.
- You can port this logic into your own codebase, then extend it to a visual web app.

---

### 2.3 Movie Recommender System using MovieLens Dataset

- **GitHub:**  
  https://github.com/abhipatel35/MovieMatcher-Movie-Recommender-System[web:90]

**Usage in project:**

- Use as a **structural reference** for a complete movie-recommender repo.
- Look at:
  - How they organize data, models, and evaluation scripts.
  - How multiple algorithms (CF, MF, maybe content-based) are compared.
- You can mirror the idea:
  - Implement SVD-based MF as the **primary model**.
  - Optionally add a simple baseline to compare in your metrics page.

---

### 2.4 Movie Recommendation System (Multiple Methods incl. MF)

- **GitHub:**  
  https://github.com/rcz7795/Movie-Recommendation-System[web:95]

**Usage in project:**

- Use to see **how MF is presented among several methods**.
- Key ideas:
  - Baselines (global mean, user–user, item–item CF) vs MF results.
  - How evaluation metrics and tables are displayed.
- Adopt the pattern of:
  - Baseline vs SVD-MF comparisons in your README and Streamlit metrics section.

---

### 2.5 Matrix Factorization for Movie Recommendations in Python (Blog)

- **Blog:**  
  https://beckernick.github.io/matrix-factorization-recommender/[web:76]

**Usage in project:**

- Use as a **conceptual and implementation guide**.
- Helpful for:
  - Understanding the math and intuition of low-rank MF for recommendations.
  - Seeing a clear, step-by-step implementation with MovieLens ratings.
  - Copying the idea of a `recommend_movies(user, n)` function returning a DataFrame.
- You can translate this notebook into:
  - A `notebooks/01_mf_baseline.ipynb` in your repo.
  - Backend functions that your app’s UI will call.

---

## 3. How to Use These in Your Repo

Recommended usage pattern:

- **`data/` folder**
  - Download MovieLens 100K and store under `data/ml-100k/`.[web:92]  
  - Optionally later add 1M under `data/ml-1m/`.

- **`notebooks/`**
  - Recreate / adapt the MF experiments from the blog and GitHub MF projects as `01_mf_baseline.ipynb`.[web:76][web:84]

- **`src/`**
  - Use MF GitHub repos as guidance for:
    - `data_loader.py` – loading and splitting MovieLens data.[web:84][web:94]  
    - `model_mf.py` – SVD/MF model training, saving, loading.  
    - `recommend.py` – functions like `get_recommendations(user_id, n)` and `get_similar_items(movie_id, n)`.

- **`app/`**
  - Once backend is ready, plug it into a Streamlit / web UI that:
    - Shows top‑N recommendations.
    - Displays metrics (RMSE, MAE, etc.) computed on MovieLens 100K/1M.

You now have a clear dataset list and project references, each with a specific role in your project.
