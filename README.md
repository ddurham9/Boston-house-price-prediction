# Boston House Price Prediction

## Project Overview

This project uses exploratory data analysis and regression modeling to predict the median value of owner-occupied homes in Boston-area towns and suburbs. The objective is to identify the variables most strongly associated with housing values and develop a regression model that can predict median home values from characteristics of a locality.

The project uses the historical Boston Housing dataset, which contains observations collected from the Boston Standard Metropolitan Statistical Area in 1970.

**Important:** The target represents the median value of owner-occupied homes within a town or suburb, measured in thousands of dollars. It does not represent the sale price of an individual property or current housing market values.

## Project Objectives

- Explore relationships between neighborhood characteristics and median housing values.
- Identify variables with the strongest relationships to housing values.
- Apply data preprocessing and feature engineering techniques.
- Build and compare Ridge regression models.
- Evaluate model performance using multiple metrics and cross-validation.
- Examine regression diagnostics, including multicollinearity and heteroskedasticity.
- Develop actionable observations from the final model.

## Dataset

The dataset contains information about Boston-area towns and suburbs. The target variable is `MEDV`, and the notebook uses the following 12 predictor variables.

| Variable | Description |
|---|---|
| `CRIM` | Per-capita crime rate by town |
| `ZN` | Proportion of residential land zoned for lots over 25,000 sq. ft. |
| `INDUS` | Proportion of non-retail business acres per town |
| `CHAS` | Charles River indicator: 1 if the tract bounds the river, otherwise 0 |
| `NOX` | Nitric oxide concentration |
| `RM` | Average number of rooms per dwelling |
| `AGE` | Proportion of owner-occupied units built before 1940 |
| `DIS` | Weighted distance to five Boston employment centers |
| `RAD` | Index of accessibility to radial highways |
| `TAX` | Full-value property tax rate per $10,000 |
| `PTRATIO` | Pupil-teacher ratio by town |
| `LSTAT` | Percentage of the population classified as lower status |
| `MEDV` | Median value of owner-occupied homes, in thousands of dollars (target) |

## Project Workflow

### 1. Exploratory Data Analysis

- Examined dataset structure, observations, and missing values.
- Analyzed the distribution of median housing values.
- Used histograms and a correlation heatmap to explore variable distributions and relationships.
- Investigated relationships between `MEDV` and the most strongly correlated predictors, including `LSTAT`, `RM`, `PTRATIO`, `INDUS`, and `TAX`.

### 2. Data Preprocessing and Feature Engineering

- Evaluated predictor distributions and skewness.
- Applied log transformations to selected skewed variables in the initial model.
- Used standard scaling for numerical predictors.
- Created second-degree polynomial features for `RM` and `LSTAT` to capture nonlinear relationships and interactions.

### 3. Model Development

Developed and compared two Ridge regression approaches:

- **Initial model:** Applied log transformations to selected predictors and standard scaling to the remaining numerical variables.
- **Final model:** Introduced second-degree polynomial features for `RM` and `LSTAT`, while scaling the remaining predictors.

The second model produced stronger results and was selected as the final model.

### 4. Model Evaluation

Evaluated model performance using:

- R-squared
- Root Mean Squared Error (RMSE)
- Mean Absolute Error (MAE)
- Mean Absolute Percentage Error (MAPE)
- Five-fold cross-validation

### 5. Regression Diagnostics

Examined important regression considerations:

- Variance Inflation Factor (VIF) to assess multicollinearity.
- Residual analysis to evaluate patterns in prediction errors.
- Breusch-Pagan test to assess heteroskedasticity.

## Final Model Performance

The final Ridge regression model with polynomial features improved performance over the initial log-transformed model.

| Metric | Final Model |
|---|---:|
| Training R-squared | 0.805 |
| Test R-squared | 0.784 |
| Mean Cross-Validation R-squared | 0.786 |
| Mean Absolute Percentage Error | 12.1% |

The close training and test R-squared values suggest that the model generalizes reasonably well to the held-out test data. The cross-validation results also indicate consistent predictive performance across the validation folds.

## Key Findings

- `RM` (average rooms per dwelling) and `LSTAT` (lower socioeconomic status percentage) were particularly important predictors in the final model.
- Polynomial combinations of `RM` and `LSTAT` produced the largest model coefficients, suggesting that their relationship with housing values is not fully captured by simple linear terms.
- `DIS`, `NOX`, `PTRATIO`, and `RAD` also showed predictive value in the final model.
- VIF analysis identified substantial multicollinearity among several predictors, particularly `PTRATIO`, `RM`, `NOX`, and `TAX`.
- Residual analysis suggested that residuals were generally centered around zero, although the Breusch-Pagan test indicated the presence of heteroskedasticity.

Ridge regression was used to help mitigate the effects of multicollinearity through L2 regularization.

## Limitations

- **Historical data:** The observations date to 1970 and do not reflect current housing markets.
- **Geographic scope:** Predictions concern median housing values at the town or suburb level, not individual property valuations.
- **Socioeconomic variables:** The dataset includes socioeconomic characteristics that reflect historical conditions and raise important concerns about bias and responsible interpretation.
- **Model assumptions:** The diagnostics identified heteroskedasticity and substantial multicollinearity, which should be considered when interpreting model coefficients.
- **Association versus causation:** Relationships identified by the model should not be interpreted as evidence that a particular characteristic causes changes in housing values.

## Technologies Used

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Statsmodels

## Repository Contents

```text
boston-house-price-prediction/
│
├── README.md
├── Boston_House_Price_Prediction.ipynb
├── Boston.csv
├── requirements.txt
└── .gitignore
```

*Note: Include `Boston.csv` in the repository only if its source and licensing terms permit redistribution. Otherwise, provide instructions for obtaining the dataset separately.*

## Conclusion

This project demonstrates an end-to-end regression workflow, from exploratory data analysis and preprocessing to feature engineering, model comparison, evaluation, and diagnostics.

The final Ridge regression model achieved a test R-squared of 0.784 and a mean cross-validation R-squared of 0.786. The results highlight the value of polynomial feature engineering when modeling nonlinear relationships in housing data, while also demonstrating the importance of evaluating model assumptions and limitations.
