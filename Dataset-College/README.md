# College Dataset Analysis

Exploratory analysis of the ISLR/ISLP `College` dataset.  
Key focus: visualizing differences in tuition and student demographics between private and public institutions.

## Quick Look

![Outstate Tuition Boxplot](figures/boxplot_outstate.png)
<img src="figures/boxplot_outstate.png" width="500">
## Highlights
- Created a new variable `Elite` using `pd.cut`.
- Visualized Out-of-State tuition by `Private`/`Public` status.
- Compared distributions of Room & Board, Personal, and Books expenses.

## Requirements

Use the below command in a terminal or notebook environment such as bash, Jupyter, or Colab:

```bash
pip install -r requirements.txt
