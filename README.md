# Olympiad Sport Analytics Challenge

An end-to-end data science project analyzing the Milan Cortina 2026 Winter Olympics athlete dataset. Covers data cleaning, exploratory analysis, medal prediction modeling, and business strategy recommendations for the North American Winter Sports Consortium.

## Project Structure

```
Olympiad/
├── README.md                                              ← You are here
├── Olympiad_Code.ipynb                                    ← Main analysis notebook (run this)
├── milan_cortina_2026_athletes.csv                        ← Raw input dataset
├── milan_cortina_2026_athletes_cleaned_eda.csv            ← Cleaned data for EDA
├── 01_Student_Problem_Statement.docx                      ← Competition brief
├── 02_Data_Cleaning_Report.pdf                            ← Task 1 written report
├── 03_EDA_Report.pdf                                      ← Task 2 written report
├── 04_Modelling_Report.pdf                                ← Task 3 written report
├── 05_Business_Insight_Report.pdf                         ← Task 4 written report
└── outputs/
    ├── plots/                                             ← All generated figures (31 PNGs)
    ├── reports/                                           ← Written analysis (6 Markdown files)
    └── tables/                                            ← Summary CSVs (25 files)
```

## How to Reproduce Results

### 1. Clone the repository

```bash
git clone https://github.com/david-shodipo-brocku/Olympiad-Sport-Analytics-Challenge.git
cd Olympiad-Sport-Analytics-Challenge
```

### 2. Install dependencies

Python 3.9+ is recommended. Install all required packages:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

No additional data downloads are needed - the raw CSV is included in the repo.

### 3. Run the notebook

```bash
jupyter notebook Olympiad_Code.ipynb
```

Then **Run All Cells** (`Kernel → Restart & Run All`).

All outputs - cleaned CSVs, plots, tables, and reports - will be written to the `outputs/` directory. Pre-generated outputs are already included so you can browse results without running the notebook.

## Dataset

**File:** `milan_cortina_2026_athletes.csv`  
**Rows:** 390 athletes (387 after duplicate removal) across 14 winter sports  
**Target variable:** `Medal` - Gold, Silver, Bronze, or None

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
| `World_Cup_Points_Preseason` | FIS/ISU World Cup points from the preceding season |
| `Country_GDP_per_capita` | GDP per capita of the athlete's nation (USD) |
| `Winter_Sport_Tradition_Index` | 0–1 index of national winter-sport culture |
| `Medal` | Outcome: Gold, Silver, Bronze, or None |

**Known planted errors corrected in Task 1:**

| Column | Bad Value | Reason Impossible |
|---|---|---|
| `Age` | 9 | No Olympic ice hockey player is 9 years old |
| `Training_Hours_Per_Week` | 172 | Exceeds the 168 hours in a week |
| `VO2max` | -8.4 | Physiologically impossible - negative oxygen consumption |
| `Body_Fat_Pct` | 99.2 | Incompatible with elite athletic performance |

## Analysis Overview

### Task 1 - Data Cleaning and Quality Audit

- **Duplicates:** 3 duplicate records identified by full-row matching (excluding Athlete_ID) and removed, reducing the dataset from 390 to 387 rows
- **Error correction:** 4 planted impossible values detected by exact match and corrected to sport-wise mean values to preserve sport-specific distributions
- **Missing data:** Variables with missing values ranged from 6% to 26%. `Reaction_Time_ms` and `World_Cup_Points_Preseason` were classified as **MNAR** (Missing Not At Random) - both are systematically absent for sports where they are not applicable. Remaining variables were classified as **MCAR** and imputed using sport-wise means
- **Outliers:** IQR and Z-score methods used. Deanna Stellato-Dudek (age 42, figure skating) and Elana Meyers Taylor (age 41, bobsleigh) were flagged but retained - both are legitimate elite veteran athletes whose removal would introduce bias
- **Feature engineering:** Three new variables created: `VO2_BodyFat_Efficiency` (VO2max / Body_Fat_Pct), `Experience_Load_Index` (Previous_Olympics × Training_Hours_Per_Week), `Resource_Tradition_Score` (GDP per capita × Winter_Sport_Tradition_Index)
- **Before / after:** 390 rows → 387 rows; 17 columns → 24 columns (including engineered features and MNAR indicators); 310 missing or blank values → 0

### Task 2 - Exploratory Data Analysis (Q2.1–Q2.6)

Six analytical questions, each answered with at least one visualization and a written interpretation:

| Question | Topic | Key Finding |
|---|---|---|
| Q2.1 | USA vs Canada head-to-head | USA won 10 gold medals vs Canada's 8. USA showed more consistent performance across metrics; Canada had a wider spread in World Cup points, relying more on standout athletes. USA fielded athletes across a broader sport portfolio. |
| Q2.2 | Profile of Gold vs Silver/Bronze vs No Medal | The gap between medallists and non-medallists is larger than the gap between Gold and Silver/Bronze. Gold medalists ranked highest on VO2max, training hours, and World Cup points. Age and reaction time showed less separation. |
| Q2.3 | Sport portfolio and 2030 investment priorities | USA excelled in freestyle skiing (100%), figure skating (80%), and bobsleigh (67%). Canada led in curling (100%), ice hockey (67%), and short track (60%). Both nations showed zero conversion in biathlon, luge, and Nordic combined. |
| Q2.4 | Age, experience, and the peak performance window | Peak medal rates in the 25–34 age band. Experience curve peaks around 4 previous Olympic appearances. Jilek (20, gold) and Stellato-Dudek (42, debut) define the outlier boundaries. |
| Q2.5 | GDP, winter-sport tradition, and Norway's dominance | GDP predicts medals more strongly in equipment-intensive sports (alpine, bobsleigh, luge) than in endurance sports (cross-country, biathlon). Norway leads simultaneously on tradition index, VO2max, and preseason points — a system-level advantage, not a single variable. |
| Q2.6 | Physiological signature of champions | VO2max–training-load relationship plateaus at high volumes, consistent with overtraining effects. Medalist VO2max thresholds vary significantly by sport (cross-country medalists avg 93.9 vs curling medalists avg 53.6). Canadian medalists showed slightly higher VO2max than USA medalists; USA medalists showed a tighter, higher-centred distribution. |

### Task 3 - Medal Prediction Model

- **Target:** `Medal_Binary` - 1 if any medal, 0 if no medal
- **Class imbalance:** ~27% of athletes won a medal; addressed using `class_weight="balanced"` in all models
- **Pipeline design:** Train/test split (80/20, stratified) performed **before** imputation to prevent data leakage. All preprocessing (median imputation, standard scaling, one-hot encoding) applied inside the sklearn Pipeline and fitted on the training fold only
- **Models trained:** Logistic Regression (baseline) and Random Forest
- **Best model:** Logistic Regression at threshold 0.475

| Model | Accuracy | Precision | Recall | F1 | AUC-ROC |
|---|---|---|---|---|---|
| Logistic Regression | 0.782 | 0.567 | 0.810 | 0.667 | 0.845 |
| Random Forest | 0.795 | 0.647 | 0.524 | 0.579 | 0.815 |

Logistic Regression was selected as the operational model because recall is the decisive metric in this context - missing a genuine medalist is a more costly error than over-predicting. Its recall advantage (0.81 vs 0.52) outweighed Random Forest's marginal accuracy gain.

**Top predictors:** Sport type dominated (Cross-Country, Curling, Biathlon, Freestyle Skiing, Luge). Among numeric features: VO2max, Training_Hours_Per_Week, and Previous_Olympics were the strongest individual signals. World Cup preseason points had ~25% missingness; its MNAR indicator absorbed much of its signal.

**Required 7-athlete prediction test results:**

| Athlete | Country | Predicted Probability | Predicted | Actual | Correct? |
|---|---|---|---|---|---|
| Jordan Stolz | USA | 0.94 | Medal | Gold | ✓ |
| Mikaela Shiffrin | USA | 0.93 | Medal | Medal | ✓ |
| Elana Meyers Taylor | USA | 0.91 | Medal | Gold | ✓ |
| Metodej Jilek | CZE | 0.95 | Medal | Gold | ✓ |
| Courtney Sarault | CAN | 0.64 | Medal | Silver | ✓ |
| Lucas Pinheiro Braathen | BRA | 0.50 | Medal | Gold | ✓ |
| Connor McDavid | CAN | 0.27 | No Medal | Silver | ✗ |

McDavid's miss reflects the model's known limitation with team sports: individual athlete data cannot capture team dynamics, tournament bracket effects, or match-up outcomes that drive the difference between gold and no medal in ice hockey.

### Task 4 - Business Insight Report

Standalone executive brief for the North American Winter Sports Consortium covering the Milan Cortina 2026 results and 2030 planning priorities.

**Key numbers:**
- USA medal conversion rate: **50.0%** (23 medals from 46 athletes)
- Canada medal conversion rate: **37.5%** (18 medals from 48 athletes)
- Gap: **12.5 percentage points** — an efficiency problem, not a roster-size problem

**Three key findings:**
1. Preseason World Cup form is the strongest observable predictor. Gold medalists entered Milan Cortina with a mean of 679 World Cup points vs 574 for non-medalists - a signal observable months before competition
2. Physiology is sport-specific. Gold medalists averaged VO2max of 78.9 vs 65.1 for non-medalists overall, but cross-country medalists averaged 93.9 while curling medalists averaged 53.6 - a single universal benchmark misallocates resources
3. Country systems provide a baseline, but individual development pathways can override them. Braathen's gold for Brazil reflects development through the Norwegian system, not a Brazilian winter-sport program

**Three recommendations:**
1. Direct funding toward athletes already ranked in the top of international competition, not broad roster expansion
2. Set sport-specific performance benchmarks for VO2max, training load, and preseason competition form rather than universal fitness standards
3. Use October/November World Cup results as an early-warning system to target late-season coaching, equipment, and recovery investment

**Uplift estimate:** Closing 25% of the USA–Canada medal-rate gap → approximately **1.5 additional medals**. Closing 50% → approximately **3 additional medals**. Assumes stable 48-athlete roster and similar sport mix. Directional planning figures, not causal forecasts.

### Bonus - Multi-Class Medal Prediction

Extended model predicting Gold / Silver / Bronze / None (4 classes) using the same leakage-safe pipeline and Logistic Regression with `class_weight="balanced"`.

| Metric | Score |
|---|---|
| Accuracy | 0.551 |
| Weighted F1 | 0.624 |
| Macro F1 | 0.321 |

The None class is identified reliably. Errors concentrate among neighbouring podium classes (Gold predicted as Silver, Silver predicted as Bronze) - the expected failure pattern given that real-world margins between first and second place are fractions of a second or a judge's score, none of which exist in tabular athlete data. The binary model remains the more reliable operational tool; the multi-class version provides a useful directional signal for distinguishing likely non-medalists from likely podium contenders.

Full discussion in `outputs/reports/bonus_multiclass_model_discussion.md`.

## Key Findings

1. **Preseason World Cup points are the strongest single predictor of medal success** - athletes already near the top internationally before the Games are consistently more likely to medal, and this signal is observable months in advance
2. **Sport type is the dominant model feature** - what sport an athlete competes in matters more than any individual physiological variable because medal rates vary structurally across disciplines
3. **Physiology separates medalists from non-medalists differently by sport** - VO2max matters most in endurance disciplines (cross-country, biathlon) and least in technical disciplines (alpine skiing, figure skating, curling)
4. **The VO2max–training-load relationship plateaus** - athletes training at extreme volumes do not show proportionately higher aerobic capacity, consistent with overtraining literature
5. **Norway's dominance is system-level** - it leads simultaneously on tradition index, median VO2max, and preseason points across both equipment-intensive and endurance disciplines, not on any single variable
6. **Braathen (BRA) and McDavid (CAN) are the two hardest prediction cases** - Braathen overrides a country prior through elite individual development; McDavid illustrates the ceiling of individual-level data in team sports

## Outputs Reference

| File | Contents |
|---|---|
| `outputs/reports/task1_outlier_justification.md` | Written defence of all outlier and error decisions |
| `outputs/reports/task2_interpretations.md` | Full Q2.1–Q2.6 written analysis |
| `outputs/reports/task3_athlete_analysis.md` | Per-athlete prediction narrative for the required 7 athletes |
| `outputs/reports/task3_confusion_matrix_interpretation.md` | Confusion matrix breakdown with TP/FP/FN/TN interpretation |
| `outputs/reports/task4_business_insight_report.md` | Executive brief and six strategic insights |
| `outputs/reports/bonus_multiclass_model_discussion.md` | Multi-class model discussion |
| `outputs/tables/` | 25 summary CSVs supporting each question (missingness report, error log, outlier audit, sport archetype profiles, medal rate tables, model comparison, feature importance, and more) |
| `outputs/plots/` | 31 figures (PNG) covering all tasks |

## Collaborators

| Name | Role |
|---|---|
| James Ly | Data cleaning and report |
| Mehdi Ben-Osman | EDA |
| David Shodipo | Feature engineering, modeling, bonus challenge |
| Dhvanit Maru | Report writing, business insight report|

## License

For academic and educational use only. The dataset is synthetic and was created for the purposes of this Olympiad competition.
