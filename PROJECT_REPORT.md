# Project Report - Student Performance Prediction System

**Name:** Twinkle Ghangare  **Internship / Mentor:** Sri Nivasan Pillai  **Date:** October 10, 2026

## 1. Introduction
Student performance depends on many factors such as study time, past failures, attendance and family background. This project builds a machine learning model that predicts a student's final grade so that students at risk can be identified early.

## 2. Objective
Build a basic ML model that analyzes student-related data and predicts student performance (final grade `G3`).

## 3. Dataset
- Source: UCI Machine Learning Repository - Student Performance (mathematics course)
- Size: 395 rows, 33 columns (confirmed from `df.shape`: 395 rows, 33 columns)
- Target: `G3` (final grade, 0-20)
- Feature types: numeric (age, studytime, failures, absences, ...) and categorical (school, sex, higher, ...)

## 4. Data Cleaning
- Missing values found: 0
- Duplicate rows: 0
- Handling: numeric → median, categorical → mode (applied in code; dataset had no nulls)
- Students with `G3 = 0`: 38; kept as real cases (dropouts / absent in exam)
- Categorical columns converted with one-hot encoding

## 5. Exploratory Data Analysis
Charts are in `images/`:
1. `01_g3_distribution.png` - distribution of final grade
2. `02_g3_by_factors.png` - grade vs study time, failures, higher-education wish
3. `03_absences_vs_g3.png`
4. `04_correlation_heatmap.png`

Observations (from the charts):
- `G1` and `G2` have the strongest positive correlation with `G3` (0.80 and 0.90). Students who did well in earlier periods almost always score high in the final exam.
- Past class failures have a clear negative correlation (-0.36) with final grades. Average marks drop sharply for students with 1 or more failures.
- Students who want to pursue higher education have a noticeably higher average grade (~10.7) compared to those who do not (~6.8).
- Weekly study time shows a mild positive correlation (0.10), while lifestyle factors like frequent outings (`goout`: -0.13) and alcohol use have negative correlations.

## 6. Feature Selection
Two scenarios were compared:
- A: all features including `G1`, `G2`
- B: without `G1`, `G2`, to allow early prediction

Top features in Scenario B (`06_feature_importance.png`):
1. `absences` (0.190)
2. `failures` (0.143)
3. `health` (0.055)
4. `goout` (0.053)
5. `age` (0.044)

## 7. Model Building
- Train/test split: 80% / 20%, `random_state = 42` (316 train, 79 test)
- Models: Linear Regression, Random Forest
- Improvement: GridSearchCV on Random Forest (best parameters: `{'max_depth': None, 'min_samples_leaf': 1, 'n_estimators': 100}`)

## 8. Results
Copy the table from `results/model_results.csv`:

| Model | MAE | RMSE | R² |
|---|---|---|---|
| Linear Regression (A) | 1.598 | 2.351 | 0.730 |
| Random Forest (A) | 1.173 | 1.967 | 0.811 |
| Linear Regression (B) | 3.395 | 4.196 | 0.141 |
| Random Forest (B) | 3.082 | 3.869 | 0.270 |
| Tuned Random Forest (B) | 3.148 | 3.935 | 0.245 |

Interpretation:
MAE means the prediction is on average off by about 1.17 grade points for Random Forest (A) and 3.08 grade points for Random Forest (B). An R² of 0.811 means Random Forest (A) explains about 81% of the variation in final grades when G1 and G2 are available. In Scenario B (early prediction without prior exam marks), the Random Forest explains about 27% of the variance (R² = 0.270) with an MAE of 3.08. Scenario A is much more accurate because past exam marks directly reflect academic ability, but Scenario B is still useful early in the semester to flag at-risk students based on attendance, failures, and background.

Plots: `05_actual_vs_predicted.png`, `07_model_comparison.png`.

## 9. Prediction System
The function `predict_student()` takes student details and returns the predicted grade and a performance level (Good ≥ 15, Average 10-14, At risk < 10). Example outputs:
- `predict_student(studytime=4, failures=0, absences=2, higher="yes", Medu=4, Fedu=4)` -> 10.7 / 20 -> Average
- `predict_student(studytime=1, failures=2, absences=15, higher="no", Medu=1, Fedu=1, goout=5)` -> 8.1 / 20 -> At risk

## 10. Conclusion
Random Forest in Scenario A gave the best performance (MAE: 1.173, R²: 0.811), showing that earlier test scores are the most reliable indicators of final marks. For early detection without prior grades (Scenario B), attendance (`absences`) and past class failures were the most important features. Linear Regression struggled in Scenario B (R²: 0.141) because the relationship between student habits and final grades is non-linear.

## 11. Limitations and Future Work
- Small dataset (395 students) from a single school context
- Only the mathematics course was evaluated
- Future work: include the Portuguese language dataset, experiment with Gradient Boosting / XGBoost, and build a simple Streamlit interface for teachers
