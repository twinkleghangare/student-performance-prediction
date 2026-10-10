# Student Performance Prediction System

Internship mini project (AI / Machine Learning). Predicts a student's final grade (`G3`, 0–20) from demographic, social, and school-related data.

## Workflow

Data → Cleaning → Analysis → Feature Selection → Training → Testing → Evaluation → Prediction

## Dataset

**UCI Student Performance Dataset**

- Course: Mathematics
- Students: 395
- Columns: 33
- File used: `data/student-mat.csv` (semicolon-separated)

Dataset source: [UCI Student Performance](https://archive.ics.uci.edu/dataset/320/student+performance)

## Repository Structure

```text
student-performance-prediction/
├── data/
├── images/
├── results/
├── .gitignore
├── PRESENTATION_OUTLINE.md
├── PROJECT_REPORT.md
├── README.md
├── Student_Performance_Prediction.ipynb
└── requirements.txt
```

## How to Run

**1. Install dependencies**

```bash
pip install -r requirements.txt
```

**2. Open the notebook**

Open `Student_Performance_Prediction.ipynb` in Jupyter Notebook or Google Colab.

**3. Run all cells**

The notebook downloads the dataset if `data/student-mat.csv` is missing.

## Models

The project compares Linear Regression and Random Forest with GridSearch tuning in two scenarios:

- **Scenario A:** Includes `G1` and `G2` (earlier grades).
- **Scenario B:** Excludes `G1` and `G2` (early-warning use).

### Evaluation Metrics

- MAE (Mean Absolute Error)
- RMSE (Root Mean Squared Error)
- R² Score

## Results

See `results/model_results.csv` and `PROJECT_REPORT.md` for the evaluation results.

## Prediction System

The `predict_student(...)` function in the notebook returns a predicted grade and a performance level: Good, Average, or At risk.

Example:

```python
predict_student(studytime=4, failures=0, absences=2, higher="yes")
```

## Tools Used

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook

## Author

**Twinkle Ghangare**

[GitHub Profile](https://github.com/twinkleghangare)

## Project Repository

[Student Performance Prediction](https://github.com/twinkleghangare/student-performance-prediction)
