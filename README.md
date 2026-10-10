# Understanding Filipinos' Perceptions of Income Equality: An Ordinal Regression Analysis

**Data Analytics | R Programming | Statistical Modeling | Public Policy Analytics**

## Project Overview

Income inequality remains a major socioeconomic concern in the Philippines. However, individuals may hold different views about whether incomes should be made more equal or whether larger income differences are necessary to reward individual effort.

This project investigates how **demographic and socioeconomic characteristics are associated with Filipinos' perceptions of income equality**, using data from the World Values Survey (WVS).

The analysis applies **Cumulative Link Models (CLMs)**, a form of ordinal regression, to examine how education, employment status, income, age, sex, and ethnolinguistic background relate to attitudes toward income distribution.

Beyond identifying which factors are statistically significant, the study also examines whether the **variability of attitudes differs across population groups** through scale-extended ordinal regression.

The project was implemented in **R using R Markdown**, integrating data analysis, statistical modeling, visualizations, and research interpretation in a reproducible analytical workflow.

## 1. Research Problem

Public attitudes toward income inequality can influence the acceptance and feasibility of economic and redistributive policies.

However, it remains unclear how different socioeconomic and demographic groups in the Philippines vary in their preferences for income equality versus larger income differences.

**Central Research Question:**

Which demographic and socioeconomic factors are associated with Filipinos' perceptions of income equality, and how do these factors influence both the direction and dispersion of their attitudes?

## 2. Research Objectives

1. Examine the distribution of income-equality perceptions across demographic and socioeconomic groups.
2. Identify statistically significant predictors of income-equality attitudes using ordinal regression.
3. Evaluate the proportional-odds assumption and explore alternative model specifications.
4. Determine whether the dispersion of attitudes varies across educational, income, and age groups.
5. Interpret the statistical findings and discuss their implications for public policy.

## 3. Dataset

**Source:** World Values Survey (WVS)

**Geographic Coverage:** Philippines

**Sample Size:** 1,200 respondents

The analysis uses selected demographic, socioeconomic, and attitudinal variables from the WVS.

### Dependent Variable

**Q106 – Perception of Income Equality**

Respondents express their views on a 10-point ordinal scale:

- **1:** Incomes should be made more equal.
- **10:** Larger income differences are needed as incentives for individual effort.

Higher values indicate stronger preferences toward the individual-incentive end of the income-distribution scale.

### Independent Variables

| Variable | WVS Code | Description |
|---|---|---|
| Sex | Q260 | Male or female |
| Age | Q262 | Respondent's age group |
| Educational attainment | Q275R | Primary, secondary, post-secondary |
| Employment status | Q279 | Full-time, part-time, self-employed, and other categories |
| Income group | Q288R | Low, medium, high |
| Ethnolinguistic group | Q290_recode | Selected Philippine ethnolinguistic groups |

Additional variables considered during exploratory analysis and model development included marital status, family savings, and subjective social class.

## 4. Analytical Methodology

### Step 1: Data Preparation

- Import and inspect the WVS dataset.
- Select relevant demographic and socioeconomic variables.
- Examine missing values and category frequencies.
- Recode variables into appropriate categorical formats.
- Convert Q106 into an ordered factor for ordinal regression.

### Step 2: Exploratory Data Analysis

Descriptive statistics and visualizations were used to examine the distribution of responses and relationships among variables.

The analysis included:

- Distribution of income-equality perceptions
- Age and employment composition
- Educational attainment and income distribution
- Ethnolinguistic differences
- Relationships between income, employment, savings, and social class

These analyses provided an initial understanding of the sample and possible associations between explanatory variables and income-equality perceptions.

### Step 3: Baseline Ordinal Regression

A **Cumulative Link Model (CLM)** with a logit link was used because the dependent variable is ordinal.

Unlike ordinary linear regression, ordinal regression preserves the ranking of response categories without assuming that the distances between adjacent categories are equal.

The baseline model included:

- Sex
- Age group
- Educational attainment
- Employment status
- Income group

Additional candidate models incorporated subjective social class, financial coping, ethnolinguistic group, and marital status.

### Step 4: Model Selection

Candidate models were compared using:

- Akaike Information Criterion (AIC)
- Bayesian Information Criterion (BIC)
- Likelihood Ratio Tests (LRT)
- Model interpretability and parsimony

The analysis also examined the proportional-odds assumption through tests of nominal effects.

Because more complex nominal-effect specifications encountered convergence and threshold-ordering issues, scale effects were explored as an alternative approach.

### Step 5: Scale-Extended Ordinal Regression

Scale effects were introduced to examine differences in the dispersion of respondents' underlying attitudes.

The final model included:

**Location effects:**
- Sex
- Age group
- Educational attainment
- Employment status
- Income group
- Ethnolinguistic group

**Scale effects:**
- Educational attainment
- Income group
- Age group

This specification allows the analysis to distinguish between:

- **Location effects:** Differences in the direction of income-equality attitudes.
- **Scale effects:** Differences in how dispersed or concentrated attitudes are across groups.

### Step 6: Model Diagnostics and Interpretation

The final model was assessed using:

- Model convergence diagnostics
- Parameter accuracy and identifiability checks
- Likelihood-based model comparisons
- Coefficient estimates and confidence intervals
- Odds ratios and scale ratios
- Predicted probabilities

For visualization, predicted probabilities were summarized into three groups:

- Low: Q106 categories 1–3
- Middle: Q106 categories 4–7
- High: Q106 categories 8–10

The regression model itself retained the full 10-category ordinal outcome.

## 5. Model Selection Results

Several cumulative link models were estimated and compared.

| Model | Specification | AIC |
|---|---|---:|
| Model D | Location-only CLM with ethnolinguistic group | 5,255.349 |
| Model D_S1 | Scale effect: Income | 5,220.438 |
| Model D_S2 | Scale effect: Education | 5,233.440 |
| Model D_S3 | Scale effects: Education + Income | 5,207.488 |
| **Model D_S4** | **Scale effects: Education + Income + Age** | **5,199.603** |
| Model D_S5 | Scale effects: Education + Income + Ethnolinguistic group | 5,200.705 |

**Selected Model: Model D_S4**

Model D_S4 achieved the lowest AIC among the candidate models and demonstrated acceptable convergence and parameter identifiability based on the study's diagnostics.

The selected model suggests that accounting for differences in response dispersion improves model fit compared with the location-only specification.

## 6. Key Findings

### Finding 1: Educational attainment is significantly associated with income-equality perceptions.

Compared with respondents who attained primary education:

| Educational Attainment | Odds Ratio | p-value |
|---|---:|---:|
| Secondary | 1.233 | 0.037 |
| Post-secondary | 1.263 | 0.003 |

Respondents with secondary and post-secondary education had higher odds of falling into the individual-incentive end of the income-distribution scale.

This suggests that educational attainment is associated with differences in preferences concerning income distribution.

### Finding 2: Employment status is associated with differences in attitudes.

Respondents classified as housewives or homemakers had lower odds of falling into higher Q106 categories compared with full-time workers.

- **Odds Ratio:** 0.769
- **p-value:** 0.029

This suggests that employment circumstances may be associated with preferences for greater income equality.

### Finding 3: Ethnolinguistic differences are statistically significant.

Relative to Bicolano respondents, selected ethnolinguistic groups showed lower odds of falling into higher Q106 categories.

| Ethnolinguistic Group | Odds Ratio | p-value |
|---|---:|---:|
| Bisaya/Visayan | 0.580 | 0.001 |
| Cordillera/Northern Indigenous | 0.642 | 0.021 |
| Tagalog | 0.688 | 0.025 |

These results suggest that income-distribution attitudes vary across ethnolinguistic groups, even after accounting for the other variables included in the model.

However, these associations should not be interpreted as causal relationships.

### Finding 4: Education, income, and age influence the dispersion of attitudes.

The scale component of the final model identified significant differences in response dispersion.

| Variable | Scale Ratio | p-value |
|---|---:|---:|
| Post-secondary education | 0.708 | <0.001 |
| Medium income | 0.706 | <0.001 |
| Age 30–44 | 0.814 | 0.031 |
| Age 45–59 | 0.800 | 0.027 |

Scale ratios below 1 indicate lower estimated latent response dispersion relative to the corresponding reference groups.

This suggests that these groups exhibit more concentrated underlying attitudes toward income distribution.

### Finding 5: Some demographic factors do not significantly shift the direction of attitudes.

Sex, age group, and income group did not exhibit statistically significant location effects in the final model.

However, income and selected age groups showed statistically significant scale effects.

**An important analytical insight is that a variable may not significantly shift the direction of responses but may still be associated with differences in their dispersion.**

This illustrates the additional information provided by scale-extended ordinal regression.

## 7. Policy Implications

The findings highlight the importance of considering demographic and socioeconomic differences when developing and communicating policies related to income inequality.

Potential applications include:

**Evidence-Informed Policymaking**

Understanding differences in income-distribution attitudes may help policymakers assess the social acceptability of redistributive and market-oriented policies.

**Targeted Policy Communication**

Differences across education, employment, and ethnolinguistic groups may inform how policies are communicated to different population segments.

**Education and Economic Opportunity**

The observed association between education and income-distribution attitudes highlights the relevance of educational opportunities and labor-market experiences in understanding perceptions of inequality.

**Inclusive Policy Design**

Variation across population groups suggests that policies should account for differences in socioeconomic circumstances and public perceptions.

The findings provide descriptive and associational evidence rather than causal estimates of policy impacts.

## 8. Tools and Technologies

| Tool / Package | Purpose |
|---|---|
| R | Statistical programming and data analysis |
| R Markdown | Reproducible research and report generation |
| `ordinal` | Cumulative link models and ordinal regression |
| R statistical functions | Model comparisons, inference, and diagnostics |
| R visualization tools | Exploratory plots and statistical visualizations |
| RStudio | Development and execution environment |
| GitHub | Version control and project documentation |

The accompanying `.Rmd` file contains the analytical workflow. Refer to its package-loading statements for the complete list of R package dependencies.

## 9. How to Reproduce the Analysis

1. Download or clone this repository.
2. Install R and RStudio.
3. Open the project's `.Rmd` file in RStudio.
4. Install the required R packages identified in the source code.
5. Obtain the relevant World Values Survey dataset, subject to its access and usage conditions.
6. Update the dataset path and any required configuration in the R Markdown file.
7. Execute the R code chunks sequentially or use the **Knit** function to generate the report.

**Note:** Reproducibility depends on access to the dataset, the required R packages, and any preprocessing steps documented in the source file.

## 10. Limitations

The study has several limitations:

- The World Values Survey data are cross-sectional; therefore, the results establish associations rather than causal relationships.
- Smaller ethnolinguistic subgroups should be interpreted cautiously.
- The analysis focuses on selected demographic and socioeconomic variables.
- The low, middle, and high response groupings were used for visualization and do not replace the full ordinal response used in modeling.
- The study did not incorporate additional factors such as political trust, fairness perceptions, and income mobility.
- Future analyses may incorporate survey weights and regional variables to improve interpretation.

## 11. Future Research

Potential extensions include:

- Incorporating survey weights into the analysis.
- Exploring regional differences in income-equality perceptions.
- Examining institutional trust and perceptions of fairness.
- Comparing attitudes across different WVS waves.
- Evaluating alternative ordinal regression specifications.
- Extending the analysis to other Southeast Asian countries.

## 12. Author

**Dominique Pocholo P. de Lara**

Academic Data Analytics Project

**Research Areas:**
- Statistical Modeling
- Ordinal Regression
- Socioeconomic Data Analysis
- Public Policy Analytics
- R Programming and Reproducible Research

## 13. References and Data Source

**World Values Survey**

https://www.worldvaluessurvey.org/

**Selected Methodological References**

Christensen, R. H. B. (2025). *Cumulative link models for ordinal regression with the R package ordinal.*

https://cran.r-project.org/web/packages/ordinal/vignettes/clm_article.pdf

Gambarota, F., & Altoè, G. (2024). Ordinal regression models made easy: A tutorial on parameter interpretation, data simulation and power analysis. *International Journal of Psychology, 59*(6), 1263–1292.

https://doi.org/10.1002/ijop.13243

Liddell, T. M., & Kruschke, J. K. (2018). Analyzing ordinal data with metric models: What could possibly go wrong? *Journal of Experimental Social Psychology, 79*, 328–348.

https://doi.org/10.1016/j.jesp.2018.08.009

---

*This project was developed for academic and research purposes. The findings reflect statistical associations in the analyzed survey data and should not be interpreted as causal evidence.*
