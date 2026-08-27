# Disney Audience Persistence Analysis

**Beyond the Opening Weekend: Measuring Sustained Audience Attention in Disney Content**

A quantitative analysis examining whether initial popularity translates into sustained audience attention across **24 Disney, Pixar, and Marvel films released from 2014–2023**. The project introduces a custom **Persistence Score** derived from Google Trends search behavior and tests whether original films and franchise films differ in their ability to sustain audience interest beyond the initial release period.

**Author:** Ariana Seymourian — MS Business Analytics, UMass Amherst Isenberg School of Management

**Submitted to:** Disney Data & Analytics Women Award (DDAW), April 2026

---

## Business Question

**Does initial popularity translate into lasting audience attention, or do some content strategies produce stronger sustained interest after the initial release period?**

The analysis examines whether Disney's original and franchise films differ in how well they maintain audience attention after the initial release surge.

Rather than using opening-week performance as the sole indicator of success, this project develops a custom measure of **post-release persistence** using publicly observable search behavior.

---

## Key Finding

**Original films had a 76.3% higher average Persistence Score than franchise films.**

| Content Type | Mean Persistence Score |  n |
| ------------ | ---------------------: | -: |
| Original     |                  0.506 | 12 |
| Franchise    |                  0.287 | 12 |

The difference was statistically significant under both the primary non-parametric test and a confirmatory parametric test:

* **Mann-Whitney U:** U = 33, p = 0.013, r = 0.54
* **Welch's t-test:** t = 2.59, p = 0.011, Cohen's d = 1.11
* Both tests indicate a **large effect**
* Removing the COVID-era outlier *Soul* strengthened the result: p = 0.003, r = 0.68

The findings are **directional rather than causal** because the analysis uses a small observational sample and Google Trends as a proxy for audience attention.

---

## The Persistence Score

The project introduces a custom metric designed to measure how much audience attention remains after the initial release period.

**Persistence Score = Average Google Trends Interest (Weeks 5–12) ÷ Average Google Trends Interest (Weeks 1–4)**

The metric compares two stages of the release cycle:

* **Peak window:** Weeks 1–4 after release
* **Sustained window:** Weeks 5–12 after release

The resulting score ranges conceptually from **0 to 1**, where higher values indicate that a larger proportion of the initial search interest was sustained after the release period.

### Metric Components

The underlying persistence framework incorporates three measures of post-release behavior:

| Component        | Weight | Measurement                                                       |
| ---------------- | -----: | ----------------------------------------------------------------- |
| Half-Life        |  33.3% | Weeks required for interest to decline after the peak             |
| Post-Peak Decay  |  33.3% | Interest decline across the eight-week post-peak period           |
| Total Engagement |  33.3% | Search interest accumulated across the 12-week observation period |

A floor adjustment was applied exclusively to *Soul* because of its unusual COVID-era release conditions and Disney+ distribution strategy. Results were separately sensitivity-tested with and without this adjustment.

---

## Dataset

The final dataset contains:

* **24 Disney, Pixar, and Marvel films**
* **12 original films**
* **12 franchise films**
* Release years spanning **2014–2023**
* Balanced comparison groups

The dataset was expanded in version 5.0 to include:

**Originals:** *Zootopia, Big Hero 6, Coco*

**Franchise films:** *Thor: Ragnarok, Captain America: Civil War, Ant-Man and the Wasp*

---

## Data Sources

| Source        | Data Used                                                          | Access          |
| ------------- | ------------------------------------------------------------------ | --------------- |
| Google Trends | Weekly U.S. search interest across the 12-week post-release window | Public          |
| TMDB API      | Popularity, vote average, vote count, and film metadata            | Free API access |

Google Trends was collected using a standardized process for each film:

1. Search for the film title on Google Trends
2. Set the geographic region to the United States
3. Set the date range to the film's 12-week post-release period
4. Export the weekly search-interest data
5. Calculate the Persistence Score

TMDB metadata was retrieved through the movie endpoint and used to provide additional film-level characteristics and validation measures.

---

## Statistical Methodology

The analysis uses multiple statistical approaches to test whether the observed difference between original and franchise films is robust.

### Primary Test — Mann-Whitney U

A non-parametric comparison was used as the primary test because the sample contains only 12 films per group and does not require the assumption of normally distributed scores.

**Result:** U = 33, p = 0.013, r = 0.54

### Confirmatory Test — Welch's t-test

Welch's t-test was used as a secondary parametric test because it does not assume equal group variances.

**Result:** t = 2.59, p = 0.011, Cohen's d = 1.11

### Additional Validation

* **Shapiro-Wilk:** assessed normality within each group
* **IQR analysis:** identified potential extreme observations
* **Sensitivity analysis:** evaluated the effect of removing *Soul*
* **Spearman correlation:** compared Persistence Score against TMDB metrics to determine whether the metric captures a dimension distinct from conventional popularity and reception measures

### Outlier Handling

*Encanto* (0.897) and *Moana* (0.973) were identified as upper IQR outliers.

They were **retained rather than removed**, because the objective was to measure the actual distribution of audience persistence rather than eliminate legitimate high-performing observations.

---

## Key Analytical Insights

### 1. Original films showed substantially stronger persistence

Original films maintained significantly more audience search interest beyond the initial release period than franchise films.

The 76.3% difference suggests that **initial popularity and sustained attention may represent different dimensions of content performance**.

### 2. The result survives multiple statistical approaches

The same directional conclusion appears under both non-parametric and parametric testing, with large effect sizes under both approaches.

This convergence provides stronger evidence than relying on a single statistical test.

### 3. The finding is not explained by the COVID-era outlier alone

Removing *Soul*, an unusual Disney+ release during the COVID period, **strengthened rather than weakened** the observed difference.

This indicates that the primary finding is not dependent on that single observation.

### 4. Persistence captures a different dimension of performance

Spearman correlation testing against TMDB popularity and reception metrics produced non-significant relationships, suggesting that Persistence Score is not simply reproducing conventional popularity measures.

This supports its potential use as a complementary content-performance indicator.

---

## Business Interpretation

The analysis challenges a simple **"franchise = safer investment"** assumption by showing that franchise status and sustained audience attention are not necessarily synonymous.

For a content strategy team, the implication is not that original films should replace franchises. Rather, **long-term audience attention may deserve separate measurement from opening performance and established intellectual-property strength**.

A persistence metric could potentially complement traditional KPIs when evaluating:

* Content longevity
* Post-release audience interest
* Franchise versus original-content strategy
* Release strategy
* Marketing tail effects
* Potential catalog value

The analysis does **not** establish that original films cause stronger long-term engagement.

---

## Supporting Analysis

The repository includes additional visual analyses examining:

* Average Persistence Score by content type
* Persistence Score distribution
* Total engagement versus Persistence Score
* Persistence by release strategy
* Group-level trend relationships

The total engagement versus persistence analysis produced separate group-level relationships:

* **Franchise:** R² = 0.67
* **Original:** R² = 0.74

These relationships are descriptive and should not be interpreted as causal models.

---

## Tools & Technical Skills

* **Microsoft Excel** — data collection, data preparation, metric construction, statistical calculations, and visualization
* **Python** — statistical validation using `scipy` and `numpy`
* **Google Trends** — longitudinal search-interest data collection
* **TMDB API** — film metadata retrieval
* **Power BI / Looker Studio** — supporting visualization
* **Statistical analysis** — Mann-Whitney U, Welch's t-test, Shapiro-Wilk, IQR analysis, Spearman correlation, effect sizes, and sensitivity analysis

---

## Repository Contents

```text
├── README.md
├── Disney_Dataset.xlsx
└── Seymourian_Poster.pdf
```

### `Disney_Dataset.xlsx`

Complete dataset containing:

* Film-level metadata
* Google Trends observations
* Persistence Score calculations
* Statistical analysis
* Supporting visualizations

### `Seymourian_Poster.pdf`

Academic poster presenting the project's research question, methodology, findings, and statistical results.

---

## Reproducibility

Google Trends data can be reproduced by:

1. Opening Google Trends
2. Searching each film title
3. Selecting the United States
4. Setting the date range to the 12 weeks beginning with the film's release
5. Exporting the resulting data as CSV
6. Recalculating the Persistence Score using the methodology documented above

TMDB metadata can be reproduced using a free TMDB account and API key.

---

## Known Limitations

* **Small sample:** The analysis contains only 24 films, so findings should be interpreted as directional rather than generalizable.
* **Proxy measure:** Google Trends measures relative search interest, not actual viewing, streaming, ticket sales, or audience retention.
* **No internal Disney data:** Public data cannot capture Disney's internal engagement, subscriber, marketing, or financial metrics.
* **Observational design:** The analysis identifies an association between content type and persistence but cannot establish causation.
* **Google Trends normalization:** Search interest is relative within each query rather than an absolute measure of audience size.
* **Potential confounding:** Release strategy, marketing investment, distribution model, franchise familiarity, COVID-era conditions, and other factors may influence search persistence independently of content type.
* **TMDB limitations:** TMDB popularity and reception measures reflect public platform activity and do not directly measure long-term audience engagement.

---

## References

Mann, H. B., & Whitney, D. R. (1947). On a test of whether one of two random variables is stochastically larger than the other. *Annals of Mathematical Statistics, 18*(1), 50–60.

Kerby, D. S. (2014). The simple difference formula: An approach to teaching nonparametric correlation. *Comprehensive Psychology, 3*, 11.

Google LLC. (2024). *Google Trends* [Search interest data].

The Movie Database (TMDB). (2024). *TMDB API* [Film metadata].

---

## Author

**Ariana Seymourian**

MS Business Analytics
University of Massachusetts Amherst — Isenberg School of Management

[LinkedIn](https://www.linkedin.com/in/arianaseymourian) · [GitHub](https://github.com/aseymourian)

**Submitted to the Disney Data & Analytics Women Award (DDAW) — April 2026**

