# Archery Performance Analysis

## Overview

This project analyses tournament data from a local archery club to investigate the relationship between **archery experience and shooting accuracy**.

The main question was:

> **How long does it take to become a good archer?**

Since "good archer" is not precisely defined, this analysis uses **accuracy**, calculated as the proportion of arrows that successfully hit the target, as a measure of archery performance.

The analysis was completed as part of **MATHS 7107 – Data Taming** using **R and R Markdown**.

## Objectives

The analysis aims to:

* Clean and de-identify the archery tournament data.
* Calculate each archer's experience in days.
* Calculate shooting accuracy.
* Explore the distributions of experience and accuracy.
* Investigate the relationship between experience and accuracy.
* Apply a Box-Cox transformation to improve the linear modelling assumptions.
* Fit a linear regression model.
* Predict expected accuracy for different levels of archery experience.
* Provide 90% confidence intervals for the predictions.

## Dataset

The dataset contains information about **555 archers** from one tournament venue.

The original dataset contains three variables:

| Variable    | Description                                     |
| ----------- | ----------------------------------------------- |
| `Archer`    | Name of the archer                              |
| `Commenced` | Date the archer started practising archery      |
| `RES`       | Number of arrows shot and number of target hits |

To protect participants' identities, the original `Archer` column was removed and replaced with a unique numerical `ID`.

The `RES` variable was also separated into:

* `arrows` – total number of arrows shot
* `targets` – total number of successful hits

Two observations were identified as having unrealistic experience values equivalent to approximately 125 years of archery experience and were removed during data cleaning.

After cleaning, **553 observations** remained. A reproducible random sample of **450 archers** was then selected using the student number as the random seed.

## Methodology

The analysis followed these main steps:

1. **Data loading and inspection**
2. **De-identification of participants**
3. **Data transformation and cleaning**
4. **Random sampling**
5. **Accuracy calculation**
6. **Descriptive statistics**
7. **Standardisation of numerical variables**
8. **Distribution and skewness analysis**
9. **Scatterplot and relationship analysis**
10. **Box-Cox transformation**
11. **Linear regression modelling**
12. **Model assumption checking**
13. **Accuracy prediction with 90% confidence intervals**

The analysis used R packages including:

* `tidyverse`
* `inspectdf`
* `stringr`
* `lubridate`
* `caret`
* `moments`
* `tinytex`

## Key Findings

The mean archery experience in the sample was approximately **5,406 days**, while the mean accuracy was **0.708**, meaning that the average archer hit approximately 70.8% of their shots.

The analysis found a strong positive relationship between experience and accuracy. However, the initial relationship appeared somewhat curved, with improvements in accuracy becoming less pronounced as experience increased.

A Box-Cox transformation was therefore applied to accuracy. The estimated transformation parameter was:

**λ = 2.4**

The transformation reduced the skewness of accuracy from approximately **-0.636 to -0.127**, producing a more suitable response variable for linear modelling.
The fitted linear model was:

```text
y* = -0.386 + 3.07 × 10⁻⁵x
```

where `y*` is the Box-Cox transformed accuracy and `x` is the number of days of archery experience.

The model produced an **R² of approximately 0.947**, indicating a strong association between experience and transformed accuracy in this sample.

## Predicted Accuracy

The model was used to estimate accuracy for archers with different amounts of experience. The predictions were transformed back to the original accuracy scale.

| Experience | Predicted Accuracy | 90% Confidence Interval |
| ---------: | -----------------: | ----------------------: |
|    2 years |              0.424 |           0.413 – 0.434 |
|    5 years |              0.520 |           0.513 – 0.526 |
|   10 years |              0.640 |           0.636 – 0.643 |
|   15 years |              0.734 |           0.732 – 0.737 |
|   20 years |              0.815 |           0.812 – 0.817 |
|   25 years |              0.885 |           0.882 – 0.888 |

These predictions suggest that accuracy improves substantially with experience, particularly during the earlier years of training. The confidence intervals become narrower for higher levels of experience in this dataset.

## Conclusion

There is no single point at which someone becomes a "good archer", because this depends on how good performance is defined.

Using **88.5% accuracy** as an example threshold for a good archer, the model predicts that approximately **25 years of experience** would be required to reach this level of accuracy.

However, this result should be interpreted cautiously. The linear model assumes that accuracy continues to increase with experience, which may not be realistic indefinitely. For example, applying the model to 40 years of experience produces a predicted accuracy greater than 100%, which is impossible. Other factors such as physical condition and individual differences may also influence archery performance but are not included in the model.

Therefore, the analysis provides evidence that **greater archery experience is strongly associated with higher accuracy**, but it should not be interpreted as proof that an archer must train for a particular number of years to become good.

## Repository Structure

```text
Archery-Performance-Analysis/
│
├── README.md
├── Report/
│   └── Archery_Analysis_Report.pdf
│
├── Data/
│   └── archery_2.csv
│
└── SRC/
    └── archery_analysis.Rmd
```

## Tools

**Language:** R

**Report:** R Markdown → PDF

**Main libraries:** `tidyverse`, `lubridate`, `caret`, `moments`, `inspectdf`, `stringr`

## Author

**Chuafa Vachoima**

MATHS 7107 – Data Taming
University of Adelaide
