# disney-audience-persistence-analysis
Custom Persistence Score analysis measuring sustained audience engagement across 24 Disney/Pixar/Marvel films using Google Trends and TMDB data. Mann-Whitney U + Welch's t-test validation.
Disney Audience Persistence Analysis
Beyond the Opening Weekend: Measuring Sustained Audience Engagement in Disney Content
A custom quantitative analysis measuring long-term audience retention across 24 Disney, Pixar, and Marvel films (2014–2023) using a custom-built Persistence Score metric derived from Google Trends search behavior.

Key Finding
Original films score 76.3% higher on the Persistence Score than franchise films (mean: 0.506 vs. 0.287, n=12 per group).

Mann-Whitney U test: U=33, p=0.013 (one-tailed), r=0.54 (large effect)
Confirmatory Welch's t-test: t=2.59, p=0.011, Cohen's d=1.11 (large effect)
Both tests independently significant — convergent evidence across parametric and non-parametric methods
Sensitivity check excluding Soul (COVID-era outlier): p=0.003, r=0.68 (highly significant)


Research Question
Does initial popularity translate to lasting audience engagement — or does something else drive long-term content success? This project challenges the conventional franchise-first assumption in studio content strategy by measuring sustained audience attention rather than peak performance.

The Persistence Score
A custom metric built from Google Trends weekly search interest data.
Persistence Score = Avg Google Trends Interest (Weeks 5–12) ÷ Avg Google Trends Interest (Weeks 1–4)

Peak window: Weeks 1–4 (release momentum)
Sustained window: Weeks 5–12 (long-term retention)
Range: 0 (immediate decay) → 1 (near-perfect retention)
Higher score = stronger long-term audience engagement relative to peak interest

Component weights:
ComponentWeightHalf-Life (weeks post-peak)33.3%Post-Peak Decay Rate (8 weeks)33.3%Total Engagement (12 weeks)33.3%
Floor adjustment (×0.5) applied exclusively to Soul — COVID-era Disney+ exclusive, sensitivity-tested separately.

Dataset

Films: 24 Disney/Pixar/Marvel films released 2014–2023
Groups: n=12 franchise films, n=12 original films (balanced)
New in v5.0: Zootopia, Big Hero 6, Coco (originals); Thor: Ragnarok, Captain America: Civil War, Ant-Man and the Wasp (franchise)


Data Sources
SourceData CollectedAccessGoogle TrendsWeekly search interest, U.S., 12-week window per film from release datePublic — no API key requiredTMDB APIFilm metadata: popularity score, vote average, vote countFree API key required — register at themoviedb.org
How to Reproduce the Google Trends Data

Go to trends.google.com
Search each film title
Set the date range to the 12-week window starting from the film's release date
Set region to United States
Export as CSV

How to Access TMDB Data

Create a free account at themoviedb.org
Request a free API key from your account settings
Use the /movie/{movie_id} endpoint to retrieve popularity, vote_average, and vote_count
Full API documentation: developers.themoviedb.org


Statistical Methods
TestPurposeResultMann-Whitney U (primary)Non-parametric group comparison, no normality assumptionp=0.013, r=0.54 (large effect)Welch's t-test (secondary)Parametric confirmatory test, unequal variancesp=0.011, d=1.11 (large effect)Shapiro-WilkNormality checkNon-significant (n=12 per group, low power)IQR Outlier DetectionIdentify extreme valuesEncanto (0.897) and Moana (0.973) flagged as upper outliers — retainedSensitivity AnalysisTest robustness after removing Soulp=0.003, r=0.68 (strengthens)Spearman CorrelationValidate against TMDB metricsAll non-significant — confirms Persistence Score measures distinct dimension

Tools Used

Microsoft Excel — data collection, Persistence Score calculation, chart creation, statistical analysis
Python (scipy, numpy) — statistical validation (Mann-Whitney U, Welch's t-test, Shapiro-Wilk, IQR)
TMDB API — film metadata retrieval
Google Trends — weekly search interest data collection
Power BI / Looker Studio — supporting visualizations


Repository Contents
FileDescriptionREADME.mdProject overview, methodology, and reproduction guideDisney_Dataset.xlsxFull dataset with all 24 films, Persistence Scores, and metadataSeymourian_Poster.pdfAcademic poster presented at DDAW 2026

Key Visualizations

Average Persistence Score by Content Type — Bar chart showing 76.3% gap between original and franchise films with error bars (±1 std dev)
Persistence Score Distribution — Histogram showing franchise films cluster in 0.2–0.4 range while originals spread across all bins including 0.8–1.0
Total Engagement vs. Persistence Score — Scatter plot with per-group trendlines (Franchise R²=0.67, Original R²=0.74)
Average Persistence Score by Release Strategy — Bar chart showing theatrical, hybrid, and streaming comparisons


Limitations

Sample limited to 24 Disney/Pixar/Marvel films — results directional, not causal
Google Trends provides relative, not absolute, search interest
No direct streaming data available — engagement approximated through publicly observable search behavior
TMDB variables reflect theatrical scale and critical reception rather than long-term engagement


References

Mann, H.B. & Whitney, D.R. (1947). On a test of whether one of two random variables is stochastically larger than the other. Annals of Mathematical Statistics, 18(1), 50–60.
Kerby, D.S. (2014). The simple difference formula: An approach to teaching nonparametric correlation. Comprehensive Psychology, 3, 11.
Google LLC. (2024). Google Trends [Search interest data]. trends.google.com
The Movie Database (TMDB). (2024). TMDB API [Film metadata]. themoviedb.org


Author
Ariana Seymourian
MS in Business Analytics, University of Massachusetts Amherst — Isenberg School of Management
LinkedIn · GitHub
Submitted to the Disney Data & Analytics Women Award (DDAW) — April 2026
