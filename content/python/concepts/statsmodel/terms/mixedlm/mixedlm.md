---
Title: 'MixedLM'
Description: 'MixedLM in Statsmodels is a class for fitting linear mixed-effects models, which account for both fixed and random effects in data.'
Subjects:
  - 'Data Science'
  - 'Machine Learning'
Tags:
  - 'Linear Regression'
  - 'Machine Learning'
  - 'Python'
  - 'Statistics'
  - 'Supervised Learning'
CatalogContent:
  - 'learn-python-3'
  - paths/data-science
---

**MixedLM** in Python's [Statsmodels](https://www.codecademy.com/resources/docs/python/statsmodels) library is a tool for fitting mixed-effects models, combining fixed and random effects to analyze data. It captures fixed effects (predictable factors) and random effects (unpredictable factors), defining mixed-effect modeling. Fixed effects explain the trend, while random effects account for variability across groups.

## Application of mixedlm model

- **Random Intercept Model**: Captures group-level variability in the intercept while keeping the slope fixed.
- **Random Slope Model**: Allows the slope to vary across groups to account for differences in trends.
- **Variance Components Model**: Decomposes variance into different components to understand variability sources.

## Syntax

```
import statsmodels.api as sm

model = sm.MixedLM(endog, exog, groups, exog_re=None)
```

- `endog`: Dependent variable (response).
- `exog`: Independent variables (fixed effects).
- `groups`: Grouping variable to model random effects.
- `exog_re` (optional): Design matrix for random effects.

## Example

In this example, a mixed-effects model is fitted to NBA team performance data, with `'Minutes'` as a fixed effect and `'Team'` as a random effect to analyze points scored:

```
import pandas as pd
from statsmodels.formula.api import mixedlm

# An example of the performance between two NBA teams' (team names: TeamG, TeamR)
data = pd.DataFrame({
    'Points': [10, 25, 35, 30, 22, 14, 24, 28, 32, 27],
    'Minutes': [35, 40, 30, 38, 33, 32, 34, 39, 41, 36],
    'Team': ['TeamG', 'TeamG', 'TeamR', 'TeamR', 'TeamG', 'TeamG', 'TeamR', 'TeamR', 'TeamG', 'TeamR']
})

# Fit mixed-effects model: Fixed effect for minutes played, random effect for teams
model = mixedlm("Points ~ Minutes", data, groups="Team")
result = model.fit()

# Display the results
print(result.summary())
```

The code generates the output as follows:

```shell
        Mixed Linear Model Regression Results
======================================================
Model:            MixedLM Dependent Variable: Points
No. Observations: 10      Method:             REML
No. Groups:       2       Scale:              45.7191
Min. group size:  5       Log-Likelihood:     -30.8931
Max. group size:  5       Converged:          Yes
Mean group size:  5.0
------------------------------------------------------
            Coef.  Std.Err.   z   P>|z|  [0.025 0.975]
------------------------------------------------------
Intercept    1.759   22.753 0.077 0.938 -42.835 46.353
Minutes      0.641    0.624 1.027 0.304  -0.582  1.863
Team Var    28.935    8.542
======================================================
```