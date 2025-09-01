# Boston Housing Dataset Analysis

Exploratory analysis of the ISLR/ISLP `Boston` dataset with quantitatively-labeled categorical variables. 
Key focus: Although it might be traditional to use features to predict Median Home Value (MEDV), this study will focus on using the features to predict per-capita crime rate (CRIM).  Some features are well-correlated, and many records tend to cluster onto exact points.

Google Colab notebook:  [E2_10](notebooks/E2_10.ipynb)

## Quick Look

<img src="figures/boston_scatter_figs_all.png" width="700">

## Highlights
- Per-capita crime rate (abbreviated CRIM, see Implementation Details below) has a correlative structure with many of the variables, including RAD, TAX, LSTAT, and B.  The highest pairwise correlation between any pair of the original variables was with RAD and TAX, owing to homogeneity for the class RAD = 24.
- After removing records with RAD = 24, there is more heterogeneity between CRIM and features, including RAD and TAX.  The RAD = 24 set is less heterogeneous, so it will be harder to explain the variation in the prediction from the features that we have. OLS and Lasso are performed on both populations.  Predictably, R^2 and RMSE show a better performance in predicting the crime rate in the RAD < 24 set.
- In implementing Lasso with alpha = 0.1 on the RAD < 24 set, the R^2 increased slightly while RMSE decreased slightly. This means that Lasso is reducing the effect of redundant features though it makes a simpler model. On the other hand, when applied to the RAD = 24 set, the R^2 decreased while RMSE increased. There is almost no signal to find, so shrinkage (pulling extreme observations out) adds bias without meaningful reduction in variance.
- The random forest in sklearn can handle binary indicators, but it is important to see if there is a role in the specific values in RAD. So, we perform a random forest model in two cases. The first case is where RAD is removed but leave only RAD_24, an indicator for RAD = 24. The second case is where the values of RAD are retained. Both models perform very well in terms of R^2 and RMSE; they explain a similar amount of variance to Lasso for RAD < 24 but even have a significant drop in test error as shown with RMSE. The features selected in each are basically the same.
- Drivers: The most important drivers of crime rate are MEDV, RAD, and NOX.  RAD_24 can be used in place of RAD without a difference in model performance.

## Implementation Details
- Headers are absent from the original dataset, but they are added as follows: \
    CRIM - per capita crime rate by town \
    ZN - proportion of residential land zoned for lots over 25,000 sq.ft. \
    INDUS - proportion of non-retail business acres per town. \
    CHAS - Charles River dummy variable (1 if tract bounds river; 0 otherwise) \
    NOX - nitric oxides concentration (parts per 10 million) \
    RM - average number of rooms per dwelling \
    AGE - proportion of owner-occupied units built prior to 1940 \
    DIS - weighted distances to five Boston employment centers \
    RAD - index of accessibility to radial highways \
    TAX - full-value property-tax rate per $10,000 \
    PTRATIO - pupil-teacher ratio by town \
    B - 1000(Bk - 0.63)^2 where Bk is the proportion of black people by town \
    LSTAT - percent lower status of the population \
    MEDV - Median value of owner-occupied homes in $1000's
- CHAS and RAD are categorical variables, and RAD is not binary.  The possible values of RAD within the dataset are 1,2,3,4,5,6,7,8, and 24.  The value 24 corresponds to a relatively homogeneous population whose crime rate might be difficult to predict from this dataset.  TAX has viable interpretation as a quantitative variable, but it clusters around tracts that might require treatment as categorical.
- The variable RAD_24 is a binary variable created to indicate 1 when RAD = 24 and 0 otherwise.
- As before, we use StandardScaler() to normalize values so that feature importances can be compared.
- B is a statistic derived from the proportion of black people in the town, but squaring creates a dispersion statistic that is intentionally ignorant of whether Bk was greater or less than 0.63.  This provides a more stable but potentially biased or rigid statistic.
- There is a decent but not overwhelming amount of multicollinearity in the dataset, so a Lasso hyperparameter of alpha = 0.1 was sufficient to perform feature selection.
- CHAS is already binary, so it fits naturally as a feature in the Random Forest regressor.  As said in highlights, RAD can be treated in two separate ways.

## Correlation, Error, Feature Importances by RAD
- [CRIM, RAD, TAX, B (All Records)](figures/boston_scatter_figs_all.png)
- [Correlation Heatmap (All Records)](figures/corr_matrix.png)
- [CRIM, RAD, TAX, B (RAD = 24)](figures/boston_scatter_figs_RAD=24.png)
- [CRIM, RAD, TAX, B (RAD != 24)](figures/boston_scatter_figs_RAD~=24.png)
- [Split RAD Importances](figures/Split_RAD_Importances.csv)
- [Random Forest Errors](figures/RF_Error.csv)
- [Random Forest Importances](figures/RF_Importances.csv)


## Requirements

Use the below command in a terminal or notebook environment such as bash, Jupyter, or Colab:

```bash
pip install -r requirements.txt
