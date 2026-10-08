# Wine Quality Analysis (WineQT)

Exploratory data analysis of the physicochemical properties of wine and their relationship with quality scores.

## Problem Statement

Wine quality is usually judged by human tasters, which is slow, subjective and costly to repeat at scale. Producers already measure chemical properties routinely, such as acidity, sugar, chlorides, sulphates and alcohol.

Given 1,143 wine samples, each described by 11 physicochemical measurements and a quality score from 3 to 8, this project asks:

> Which properties are associated with higher or lower quality, and is the data ready for building a predictive model?

## Objectives

1. Inspect the dataset's structure and check its quality (missing values, duplicates).
2. Study the distribution of each feature and of the quality score, including skewness and class imbalance.
3. Compare key features, especially alcohol, across quality levels.
4. Measure correlations between each feature and quality, and among the features themselves.
5. Summarize the findings and recommend preparation steps before modelling.

**Scope:** exploratory analysis only. Building and evaluating a predictive model is proposed as the next phase.

## Dataset

| Item | Detail |
|---|---|
| File | `WineQT.csv` |
| Rows | 1,143 |
| Columns | 13 (11 features, `quality`, `Id`) |
| Missing values | 0 |
| Duplicate rows | 0 |
| Target | `quality` (integer, 3 to 8) |

**Features:** fixed acidity, volatile acidity, citric acid, residual sugar, chlorides, free sulfur dioxide, total sulfur dioxide, density, pH, sulphates, alcohol.

`Id` is only a row identifier and carries no information about the wine.

## Repository Contents

| File | Description |
|---|---|
| `WineQT.ipynb` | Jupyter notebook with the full analysis |
| `WineQT.csv` | Dataset (add this yourself, see below) |
| `WineQT_Report.pptx` | 11-slide report of the analysis and findings |
| `WineQT_Problem_Statement.pptx` | 4-slide problem statement |
| `README.md` | This file |

## Requirements

- Python 3.8 or later
- Jupyter Notebook or JupyterLab
- Libraries: `pandas`, `numpy`, `matplotlib`, `seaborn`

Install the libraries with:

```bash
pip install pandas numpy matplotlib seaborn notebook
```

## How to Run

1. Place `WineQT.csv` next to the notebook.
2. In the notebook, update the data path in the loading cell. It currently points to a local Windows path:

   ```python
   df = pd.read_csv("C:/Users/USER/Downloads/WineQT.csv")
   ```

   Change it to:

   ```python
   df = pd.read_csv("WineQT.csv")
   ```

3. Start Jupyter and run all cells in order:

   ```bash
   jupyter notebook WineQT.ipynb
   ```

## Methodology

1. **Load and inspect:** preview rows, shape, data types and summary statistics.
2. **Data quality checks:** count missing values and duplicates.
3. **Distributions:** bar chart of quality counts, histograms with skewness for every column, and a swarm plot of alcohol.
4. **Comparison by quality:** violin and box plots of alcohol for each quality score.
5. **Relationships:** pair plot and correlation heatmap of all columns.

## Key Findings

- **Clean data:** no missing values and no duplicate rows.
- **Imbalanced target:** about 83% of wines score 5 or 6. Grades 3, 4 and 8 are rare.
- **Alcohol** has the strongest positive correlation with quality (+0.48). Median alcohol rises from about 9.7% at quality 5 to about 11.6% at quality 7.
- **Volatile acidity** has the strongest negative correlation with quality (-0.41).
- **Other positive links:** sulphates (+0.26) and citric acid (+0.24).
- **Skewed features:** chlorides (6.03), residual sugar (4.36) and sulphates (2.50) are heavily right-skewed.
- **Correlated features:** fixed acidity is strongly related to pH (-0.69), density (+0.68) and citric acid (+0.67). Free and total sulfur dioxide are correlated at +0.66.
- No correlation with quality exceeds 0.5 in absolute value, and correlation does not prove cause.

## Known Issues in the Notebook

- `quality` is converted to a string before the violin and box plots, so those plots show categories out of numeric order (5, 6, 7, 4, 8, 3). Convert it back to an integer, or set the plot order, before later steps such as the correlation heatmap or modelling.
- `Id` is included in the histograms, pair plot and correlation heatmap. It should be dropped from these.

## Next Steps

1. **Prepare the data:** drop `Id`, transform skewed features (chlorides, residual sugar, sulphates), and scale features.
2. **Frame the target:** choose regression, or group scores into low, medium and high. Use a stratified train/test split and class weights or resampling for rare grades.
3. **Model and evaluate:** start with a linear baseline, then try Random Forest and gradient boosting. Use cross-validation and report F1 or RMSE along with feature importance.
