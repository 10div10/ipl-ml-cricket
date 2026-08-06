# 🏏 ML Cricket — IPL 2022 Performance Analysis & Prediction

<div align="center">

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML%20Models-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-Regression-2E7D32?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

**EDA + regression models that dig into IPL 2022 batting & bowling stats — and try to predict a player's Runs or Wickets from the rest of their numbers.**

[Overview](#-overview) • [Datasets](#-datasets) • [Notebooks](#-notebooks) • [Models](#-models--results) • [Getting Started](#-getting-started) • [Sample Insights](#-sample-insights) • [Roadmap](#-roadmap)

</div>

---

## 📖 Overview

`ml-cricket` analyzes the **IPL 2022** season using two official stat sheets — batting and bowling — across three notebooks:

- **`batting.ipynb`** — EDA on batting stats + regression models predicting `Runs`
- **`bowling.ipynb`** — EDA on bowling stats + regression models predicting `Wkts`
- **`final.ipynb`** — Combined exploratory analysis with the full set of visualizations (distribution plots, top-N bar charts, strike-rate comparisons, scatter plots)

<details>
<summary><b>💡 Why this project?</b></summary>
<br>

Season stat sheets are dense but flat — they don't show you who's actually driving outcomes. This project explores both datasets visually first (who scored the most, who struck fastest, who took wickets most efficiently) and then tests whether a handful of standard regressors can predict a player's headline number (Runs / Wickets) from their supporting stats.

</details>

---

## 🗂️ Datasets

| Dataset | Rows | Columns |
|---|---|---|
| `BATTING STATS - IPL_2022.csv` | 310 players | `Player, Mat, Inns, Runs, Avg, BF, SR, 100, 50, 4s, 6s` |
| `BOWLING STATS - IPL_2022.csv` | 103 players | `POS, Player, Mat, Inns, Ov, Runs, Wkts, BBI, Avg, Econ, SR, 4w, 5w` |

---

## 📊 Notebooks

<details open>
<summary><b>🏏 batting.ipynb</b></summary>
<br>

- Cleans nulls, plots `Runs` distribution and `Avg` histogram
- Features used to predict `Runs`: `Avg, Mat, BF, SR, 100, 50, 4s, 6s`
- Trains and compares **KNN, Decision Tree, Random Forest, SVR, and XGBoost** regressors
- Evaluates each model with **Mean Absolute Error (MAE)**
- Ends with a custom single-player input to sanity-check a prediction

</details>

<details>
<summary><b>🎯 bowling.ipynb</b></summary>
<br>

- Cleans nulls, plots `Wkts` distribution, `Econ` and `Avg` histograms
- Features used to predict `Wkts`: `Mat, Inns, Ov, Runs, Avg, Econ, SR, 4w, 5w`
- Same model lineup — **KNN, Decision Tree, Random Forest, SVR, XGBoost** — compared by MAE
- Ends with a custom single-player input to sanity-check a prediction

</details>

<details>
<summary><b>📈 final.ipynb</b></summary>
<br>

Pure exploratory analysis combining both datasets, including:

- Summary statistics (`describe()`) for both batting and bowling
- Filters for standout performers — centuries, 50+ scores in 3+ innings, high-boundary hitters, elite bowling combos (high wickets + low economy)
- Top-30 bar charts: matches played, most runs, most wickets
- Strike-rate vs. balls-faced line comparisons
- A `Wkts` vs. `Mat` scatter plot sized/colored by wickets taken

</details>

---

## 🤖 Models & Results

Both `batting.ipynb` and `bowling.ipynb` follow the same pipeline:

```
Feature selection → 80/20 train-test split → fit model → predict → Mean Absolute Error
```

| Model | Used for Runs (batting) | Used for Wkts (bowling) |
|---|:---:|:---:|
| K-Nearest Neighbors Regressor | ✅ | ✅ |
| Decision Tree Regressor | ✅ | ✅ |
| Random Forest Regressor | ✅ | ✅ |
| Support Vector Regressor (SVR) | ✅ | ✅ |
| XGBoost Regressor | ✅ | ✅ |

> 📌 Run the notebooks to see the actual MAE printed for each model on your machine — values depend on the `random_state` and current scikit-learn/xgboost versions, so they aren't hardcoded here. Feel free to paste your best results into the table above once you've run it.

Each notebook finishes with a **custom single-row prediction** — e.g. plugging in a hypothetical player's `Avg`, `Mat`, `BF`, `SR`, `100`, `50`, `4s`, `6s` and getting a predicted `Runs` total out of the trained XGBoost model (same idea for `Wkts` in bowling).

---

## 🔍 Sample Insights

<details>
<summary><b>Click to expand example findings from final.ipynb</b></summary>
<br>

- The dataset flags players with multiple centuries and those with 4+ half-centuries as standout batters.
- A boundary-hitting filter (`4s > 45 & 6s > 10`) isolates the season's most aggressive strikers.
- On the bowling side, filtering for `Wkts > 12` with `SR < 23` surfaces bowlers who were both prolific and efficient.
- A separate filter combining high overs bowled, 15+ wickets, and economy under 8 highlights the most reliable death/overall bowlers of the season.

</details>

---

## 🚀 Getting Started

<details open>
<summary><b>1️⃣ Clone the repo</b></summary>

```bash
git clone https://github.com/YOUR_USERNAME/ml-cricket.git
cd ml-cricket
```
</details>

<details>
<summary><b>2️⃣ Set up your environment</b></summary>

```bash
python -m venv tf_env
source tf_env/bin/activate      # Windows: tf_env\Scripts\activate
pip install -r requirements.txt
```
</details>

<details>
<summary><b>3️⃣ Update the CSV paths</b></summary>

The notebooks currently read from a local Windows path (`C:\Users\Ananya\Downloads\...`). Update the `pd.read_csv(...)` calls in each notebook to point to the CSVs in this repo, e.g.:

```python
df = pd.read_csv("BATTING STATS - IPL_2022.csv")
df1 = pd.read_csv("BOWLING STATS - IPL_2022.csv")
```
</details>

<details>
<summary><b>4️⃣ Launch the notebooks</b></summary>

```bash
jupyter notebook
```

Run `batting.ipynb` and `bowling.ipynb` for the modeling pipelines, or `final.ipynb` for the full visual breakdown.
</details>

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| **Python 3.11** | Core language |
| **Pandas / NumPy** | Data wrangling |
| **Matplotlib / Seaborn** | Visualization |
| **scikit-learn** | KNN, Decision Tree, Random Forest, SVR |
| **XGBoost** | Gradient-boosted regression |
| **Jupyter** | Interactive analysis |

---

## 🗺️ Roadmap

- [ ] Hardcode/document final MAE scores per model once tuned
- [ ] Add cross-validation instead of a single train/test split
- [ ] Try hyperparameter tuning (GridSearchCV) on the best-performing model
- [ ] Build a small Streamlit app to predict Runs/Wkts from user input interactively
- [ ] Extend to multiple IPL seasons for a proper time-series view

---

## 🤝 Contributing

Pull requests are welcome! For major changes, open an issue first to discuss what you'd like to change.

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

<div align="center">

Made with 🏏 and 🐍 by [Your Name](https://github.com/YOUR_USERNAME)

</div>
