
# Task 1 Outlier and Error Justification

## Missingness visualization
The bar chart task1_missingness_percent_bar_chart.png shows missing percentage for every column.

## Four planted errors explicitly detected and corrected
Each impossible value is named individually in task1_named_planted_errors.csv:
- Age = 9: no Olympic athlete is 8 years old
- Training_Hours_Per_Week = 172: more hours than exist in a week
- VO2max = -8.4: physiologically meaningless negative value
- Body_Fat_Pct = 99.2: incompatible with human life

All four were set to NaN and then handled through sport-wise median imputation for EDA
or fold-safe pipeline imputation for modeling.

## Real outliers retained with justification
         Athlete_Name Country          Sport  Age Medal  Previous_Olympics
Deanna Stellato-Dudek     CAN Figure Skating   43   NaN                  3
  Elana Meyers Taylor     USA      Bobsleigh   42  Gold                  3

Deanna Stellato-Dudek (42) and Elana Meyers Taylor (41) compete in figure skating and bobsled
respectively — sports where technique and experience can sustain elite performance well into the 40s.
Their ages are statistically unusual but physiologically plausible, so we keep them.
Removing them would incorrectly delete valid elite-performance data points.
