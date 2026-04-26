# Olympiad-Sport-Analytics-Challenge
An end-to-end data science project analyzing the Milan Cortina 2026 Winter Olympics athlete dataset. Covers data cleaning, exploratory analysis, medal prediction modeling, and business strategy recommendations for the North American Winter Sports Consortium.

---

## Project Structure

```
Olympiad/
├── README.md                          ← You are here
├── Olympiad_final.ipynb               ← Main analysis notebook (run this)
├── milan_cortina_2026_athletes.csv    ← Raw input dataset
└── outputs/
    ├── milan_cortina_2026_athletes_cleaned_eda.csv       ← Cleaned data for EDA
    ├── milan_cortina_2026_athletes_cleaned_model_base.csv← Cleaned data for modeling
    ├── plots/                         ← All generated figures (31 PNGs)
    ├── reports/                       ← Written analysis (6 Markdown files)
    └── tables/                        ← Summary CSVs for each question
```

---

## How to Reproduce Results

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/Olympiad-Sport-Analytics-Challenge.git
cd Olympiad-Sport-Analytics-Challenge
```

### 2. Install dependencies

Python 3.9+ is recommended. Install all required packages:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy statsmodels jupyter
```

> No additional data downloads are needed — the raw CSV is included in the repo.

### 3. Run the notebook

```bash
jupyter notebook Olympiad_final.ipynb
```

Then **Run All Cells** (`Kernel → Restart & Run All`).

All outputs — cleaned CSVs, plots, tables, and reports — will be written to the `outputs/` directory. Pre-generated outputs are already included so you can browse results without running the notebook.

---

## Dataset

**File:** `milan_cortina_2026_athletes.csv`
**Rows:** ~400 athletes across 15+ winter sports
**Key columns:**

| Column | Description |
|---|---|
| `Athlete_ID` | Unique identifier |
| `Athlete_Name` | Full name |
| `Country` | Nation (3-letter code) |
| `Gender` | M / F |
| `Age` | Age at time of Games |
| `Sport` | Discipline (e.g., Alpine Skiing, Biathlon) |
| `Previous_Olympics` | Number of prior Games attended |
| `Training_Hours_Per_Week` | Weekly training load |
| `Altitude_Training_m` | Altitude of primary training base (metres) |
| `Body_Fat_Pct` | Body fat percentage |
| `VO2max` | Aerobic capacity (mL/kg/min) |
| `Reaction_Time_ms` | Reaction time (milliseconds) |
| `Career_Injuries` | Number of career injuries |
| `World_Cup_Points_Preseason` | FIS World Cup points from the preceding season |
| `Country_GDP_per_capita` | GDP per capita of the athlete's nation (USD) |
| `Winter_Sport_Tradition_Index` | 0–1 index of national winter-sport culture |
| `Medal` | Outcome: `Gold`, `Silver`, `Bronze`, or `None` |

**Known planted errors corrected in Task 1:**
- `Age = 9` - no Olympic athlete is 9 years old
- `Training_Hours_Per_Week = 172` - exceeds hours in a week
- `VO2max = -8.4` - physiologically impossible
- `Body_Fat_Pct = 99.2` - incompatible with elite athletic performance

---

## Analysis Overview

### Task 1 - Data Cleaning & Quality Audit
- Identified and corrected four planted impossible values
- Visualized missingness patterns; flagged MNAR (Missing Not At Random) in `VO2max` by sport
- Retained real statistical outliers (Deanna Stellato-Dudek, age 42; Elana Meyers Taylor, age 41) with written justification
- Applied sport-wise median imputation for EDA; fold-safe pipeline imputation for modeling

### Task 2 - Exploratory Analysis (Q2.1–Q2.6)
Six analytical questions, each with a written interpretation and supporting tables/plots:

| Question | Topic |
|---|---|
| Q2.1 | USA vs Canada head-to-head comparison |
| Q2.2 | Profile of Gold vs Silver/Bronze vs No Medal athletes |
| Q2.3 | Sport portfolio: where should each nation focus for 2030? |
| Q2.4 | Age and experience effects on medal probability |
| Q2.5 | GDP and winter-sport tradition as predictors of national success |
| Q2.6 | Physiological signatures — VO2max, training load, and the overtraining plateau |

### Task 3 - Medal Prediction Model
- Binary classification: medal vs no medal (leakage-safe pipeline)
- Models evaluated: Logistic Regression, Random Forest, Gradient Boosting
- Best model: Logistic Regression at threshold 0.48 (AUC reported in `task3_model_comparison_leakage_safe.csv`)
- Required athlete predictions for 7 named athletes including Mikaela Shiffrin, Connor McDavid, and Lucas Pinheiro Braathen
- Written confusion matrix interpretation in `outputs/reports/task3_confusion_matrix_interpretation.md`

### Task 4 - Business Insight Report
Standalone one-page brief for the North American Winter Sports Consortium, covering:
- USA (50.0%) vs Canada (37.5%) medal conversion gap
- Three key findings: preseason form, sport-specific physiology, country systems
- Three actionable recommendations for 2030
- Explicit uplift estimate: closing 50% of the gap ≈ 3.0 additional medals

### Bonus - Multi-Class Medal Prediction
Extended model predicting Gold / Silver / Bronze / None (4 classes).
- Accuracy: 0.551 | Weighted F1: 0.624 | Macro F1: 0.321
- Discussion in `outputs/reports/bonus_multiclass_model_discussion.md`

---

## Key Findings

1. **Preseason World Cup points are the strongest single predictor of medal success** — athletes already near the top internationally before the Games are consistently more likely to medal.
2. **Physiology separates medalists from non-medalists differently by sport** — VO2max matters most in endurance disciplines (cross-country, biathlon); less so in technical disciplines (alpine skiing, figure skating).
3. **The VO2max–training-load relationship plateaus** — athletes training at extreme volumes do not show proportionately higher aerobic capacity, consistent with overtraining literature.
4. **Lucas Braathen (BRA) and Metodej Jilek (CZE) are the hardest cases** — both override their country/age priors through elite individual development pathways.
5. **Norway's dominance is system-level** — leads simultaneously on tradition index, median VO2max, and preseason points across both equipment-intensive and endurance disciplines.

---

## Outputs Reference

| File | Contents |
|---|---|
| `outputs/reports/task1_outlier_justification.md` | Written defence of outlier decisions |
| `outputs/reports/task2_interpretations.md` | Full Q2.1–Q2.6 written analysis |
| `outputs/reports/task3_athlete_analysis.md` | Per-athlete prediction narrative |
| `outputs/reports/task3_confusion_matrix_interpretation.md` | Confusion matrix breakdown |
| `outputs/reports/task4_business_insight_report.md` | Executive brief + recommendations |
| `outputs/reports/bonus_multiclass_model_discussion.md` | Multi-class model discussion |
| `outputs/tables/` | 25 summary CSVs supporting each question |
| `outputs/plots/` | 31 figures (PNG) covering all tasks |

---

## Collaborators

| Name | GitHub |
|---|---|
| *(Dhvanit Maru)* | `@username` |
| *(Mehdi Ben-Osman)* | `@username` |
|*(James Ly)* | `@username` |

---

## License

For academic and educational use only. Dataset is synthetic and created for the purposes of this Olympiad competition.
