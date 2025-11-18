
# Predicting Baseball Hitter Performance Using Component Skills

A machine learning project to predict a baseball player's future offensive performance (`xwOBA`) using a curated set of underlying "component skills" from Statcast.


---

## Project Goal

The idea for this project was to see if a holistic model built on a component hitting skills (bat speed, plate discipline, timing, barrel control, etc.) can more accurately predict future performance than a comprehensive statcast stat like barrel rate or average exit velocity.

## Data Source

The dataset is an aggregated CSV of player-seasons from 2023-2025, sourced from [Baseball Savant](https://baseballsavant.mlb.com/statcast_search).

**View the complete analysis in the Jupyter Notebook:** [notebooks/hitting_skill_ML.ipynb](notebooks/hitting_skill_ML.ipynb)

---

## Workflow

1.  **Data Cleaning & Exploration:** Loaded the data and performed an initial exploratory data analysis (EDA), including a correlation matrix to understand the initial relationships between features.
2.  **Feature Selection & Engineering:** Collaboratively selected a final set of 7 features to represent four key component skills. A new `discipline_ratio` feature (`Z-Swing% / O-Swing%`) was engineered to better capture a player's plate discipline.
3.  **Time-Based Splitting:** The data was split chronologically to create a robust validation strategy:
    *   **Training Set:** 2023-2024 Seasons
    *   **Validation Set:** 2025 Season
4.  **Modeling:** A Random Forest Regressor was trained on the training set to learn the complex, non-linear relationships between the component skills and the target variable (`xwOBA`).
5.  **Evaluation & Benchmarking:** The model's performance was evaluated on the unseen 2025 validation data and benchmarked against simpler, single-feature Linear Regression models using more comprehensive statcast stats thought to be linked to hitting performance.

---

## Key Results & Findings

The final Random Forest model successfully predicted 2025 `xwOBA` with a **Root Mean Squared Error (RMSE) of 0.0199**.

This result proved the initial hypothesis, as the model was **~7% more accurate** than the best-performing single-feature baseline model (which used `barrel_batted_rate` and had an RMSE of 0.0213).

A key insight from the analysis was that some features with high event-level value (like `squared_up_contact`) have a low player-level correlation with `xwOBA`, highlighting the complex "Power vs. Contact" trade-offs that the machine learning model successfully learned.

## Technologies Used
- Python
- Pandas
- Scikit-learn
- Seaborn & Matplotlib
- Jupyter Notebook
