# College Dataset Analysis

Exploratory analysis of the ISLR/ISLP `College` dataset.  
Key focus: visualizing differences in tuition and student demographics between private and public institutions.

## Quick Look

<img src="figures/boxplot_outstate.png" width="500">

## Highlights
- Created a new variable `Elite` using `pd.cut`.
- Visualized Out-of-State tuition by `Private`/`Public` status.
- Compared distributions of Room & Board, Personal, and Books expenses.

## Observations About Details
- The variable 'Private' is a categorical indicator, i.e. each record is Yes or No for this variable.  The rest are numerical.
- Preprocess categorical features through a one-hot encoding, as they are unordered. (TBD)
- Linear regression and neural nets rely on all variables being numerical, so the one-hot encoding is required to incorporate this variable. (TBD)
- Tree-based methods like Random Forests can handle the mixed data directly without a need for the one-hot encoding. (TBD)
- Preprocess numerical features by normalizing if using distance-based or gradient-based methods. (TBD)

## Requirements

Use the below command in a terminal or notebook environment such as bash, Jupyter, or Colab:

```bash
pip install -r requirements.txt
