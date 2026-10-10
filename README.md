# Student Performance Prediction System

Internship mini project (AI / Machine Learning). Predicts a student's final grade (`G3`, 0-20) from demographic, social and school-related data.

## Workflow
Data → Cleaning → Analysis → Feature Selection → Training → Testing → Evaluation → Prediction

## Dataset
UCI *Student Performance* dataset (mathematics course, 395 students, 33 columns):
https://archive.ics.uci.edu/dataset/320/student+performance
File used: `data/student-mat.csv` (semicolon-separated).

## Repository structure
```
├── Student_Performance_Prediction.ipynb   # full code, step by step
├── data/student-mat.csv                   # dataset
├── images/                                # saved visualizations
├── results/model_results.csv              # evaluation metrics
├── PROJECT_REPORT.md                      # project report
├── PRESENTATION_OUTLINE.md                # final presentation outline
├── requirements.txt
└── README.md
```

## How to run
1. `pip install -r requirements.txt`
2. Open `Student_Performance_Prediction.ipynb` in Jupyter or Google Colab.
3. Run all cells (the notebook downloads the dataset if `data/student-mat.csv` is missing).

## Models
Linear Regression and Random Forest (with GridSearch tuning), compared in two scenarios:
- **A:** with `G1`, `G2` (earlier grades)
- **B:** without `G1`, `G2` (early-warning use)

Metrics: MAE, RMSE, R².

## Results
See `results/model_results.csv` and `PROJECT_REPORT.md`.

## Prediction system
`predict_student(...)` in the notebook returns a predicted grade and a level (Good / Average / At risk).

```python
predict_student(studytime=4, failures=0, absences=2, higher="yes")
```

## Tools
Python, Pandas, NumPy, Matplotlib, Scikit-learn, Jupyter Notebook.
