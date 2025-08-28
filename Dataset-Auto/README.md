# Auto Dataset Analysis

Exploratory analysis of the ISLR/ISLP `Auto` dataset with qualitative variables.  
Key focus: understanding differences in Auto performance based on origin.  The performance characteristics are highly correlated.

Google Colab notebook:  [E2_9](notebooks/E2_9.ipynb)

## Quick Look

<img src="figures/boxplotCompany.png" width="700">

## Highlights
- Found heavy correlation between cylinders (number of cylinders), displacement (engine size, broadly speaking), horsepower, and weight.  These are anticorrelated with mpg and acceleration.
- Mpg is somewhat positively correlated with year, indicating potential technological advancement.
- Mpg is generally lower for American cars in aggregate, but also lower mpg when looking at the manufacturer level.
- OLS performs relatively well for predicting Mpg on American cars from quantitative features.  Most important features appear to be weight and year, across regions.
- Sparse analysis through Lasso shows similar important features.  Acceleration is much less predictive of mpg.
- Random forest with qualitative Origin variable attached shows origin not at all a driver of mpg.

## Implementation Details
- Some horsepowers are recorded as `?`, which are removed from analysis.
- Many cars with the same name are featured in different years; a couple with the same name are featured in the same year.  Each entry has remarkably different specifications, so they are treated as different data points, though names are updated to distinguish them on identification.
- Company names are extracted from names of cars for EDA; some company names are spelled incorrectly and need to be fixed.  Company names were fixed by hand.
- Lasso is performed with alpha = 0.2, a moderately high regularization parameter.  This was required due to a high degree of correlation between features.  The resulting model helped to identify important features but will have more natural bias than the OLS model.
- To implement the Random Forest regressor in scikit-learn (sklearn), the categorial variable for Origin needs to be replaced with a one-hot encoding.  That is, the three possibilities are spread out over three binary columns that are treated as separate features.  It will be interesting to know if there is a way to avoid the process of one-hot encoding, as there is a natural correlation between the resulting features.

## Feature Importances
- [OLS Performance](figures/OLSErr.csv)
- [OLS Importances](figures/OLSImportances.csv)
- [Lasso Performance](figures/LassoErr.csv)
- [Lasso Importances](figures/LassoImportances.csv)
- [Random Forest Importances](figures/RFImportances.csv)


## Requirements

Use the below command in a terminal or notebook environment such as bash, Jupyter, or Colab:

```bash
pip install -r requirements.txt
