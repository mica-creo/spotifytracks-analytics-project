# Decision Log

A running record of the key analytical choices made across the Spotify popularity project. 
---

## Assignment 2 — Dataset Proposal 
**Date:** (2026-07-19)

We chose the Spotify Tracks Dataset (Kaggle, Maharshi Pandya) because the team shares an interest in music and the dataset offered both categorical variables (explicit content, mode) and a wide set of continuous audio features (tempo, energy, danceability, loudness, valence, etc.) across ~114,000 real, unmodified tracks. 

Key Decisions: 
We selected **popularity** (0–100) as our main variable of interest because it lets us investigate which audio characteristics are associated with a song's success on Spotify. We considered danceability as an alternative main variable but felt popularity gave us a more causal, business-relevant question that could allow us to make meaningful predictions: what audio elements make a song popular?

---

## Assignment 3 — Descriptive Statistics
**Date:** (2026-07-26)

Cleaning process: 
We removed 1 row with null values and 24,259 duplicate rows (exact track_id duplicates), leaving 89,740 unique tracks. We were interested in 'genre' as a predictor, but it contained over 100 categories. We attempted to consolidate the genre variable into broader categories using AI-assisted grouping, but the groupings introduced too much inaccuracy. Thus, we decided to keep genre at full granularity rather than mislabel tracks.

Most surprising pattern: 
A large cluster of tracks with popularity = 0. This looked like a true outlier rather than a real signal of low popularity. We later confirmed in Assignment 5 it was driven largely by duplicate/compilation-album uploads rather than genuinely unpopular tracks, but left it initially because we believed from the dataset that a popularity of 0 was common (we initially hypothesized it reflected the ability of virtually anyone to upload a song to Spotify).


---

## Assignment 4 — Probability
**Date:** (2026-07-26)

Normal vs. Empirical, and Why: 
None of our variables were normally distributed in a way that would justify a normal-theory approach without caveats. Popularity has a large spike near zero and multiple mid-range peaks rather than a bell shape; duration, speechiness, acousticness, instrumentalness, and liveness are all strongly right-skewed with heavy tails; energy and loudness are left-skewed; and tempo, while close to normal on skewness/kurtosis alone, still shows irregular peaks and a concentration at zero. Because so few variables met the normality assumption, we treated the empirical/large-sample approach as the more defensible one going forward rather than assuming normal theory applies, leaning on our large sample size (n = 89,740) to justify inference later.

Probability framing:
We modeled danceability under a normal approximation to estimate the share of tracks in dance-oriented vs. mainstream vs. listening-focused popularity/streaming tiers.

---

## Assignment 5 — Statistical Inference
**Date:** (2026-08-09)

We set **α = 0.05** for both hypothesis tests. We tested whether mean danceability exceeds 0.55 
(t = 20.63, p ≈ 0 → reject H₀; sufficient evidence the population mean exceeds 0.55) 
We also tested whether mean popularity exceeds 30 (sample mean = 33.20 → reject H₀; sufficient evidence the population mean exceeds 30). 
Our 95% confidence interval placed the true mean popularity between 33.06 and 33.33 — a surprisingly tight interval given popularity ranges 0–100, which we attributed to our very large sample size and the nature of the **popularity** variable's limited 0-100 scale. 

Surprising results: The result that surprised us most was how much the spike of 0-popularity tracks was skewing our sense of "typical" popularity. After exploring individual instances of '0' **popularity**, most actually turned out to be otherwise popular artists. Individual track research showed us that many 0-popularity tracks had duplicate versions on unpopular Spotify-generated compilation albums, and were being treated as a unique track. 

Key Decision: Despite leaving the 0 observations in Assignment 2, we moved toward excluding popularity = 0 in later modeling rather than treating it as a true data point.

---

## Assignment 6 — Regression Analysis
**Date:** (2026-08-12)

Significance level: **α = 0.01** (rather than the standard 0.05) 
Given our large sample size, it was easy for very small effects to appear statistically significant, so we chose a stricter **α

Initial Model: (all candidate predictors, encoded Explicit as 0/1 and Time Signature as dummies) → R² = 0.0352. 

Model 2: We re-ran the model with all variables on the popularity > 0 sample (per the A5 decision), and doubled our R² to 0.0747. This became the working sample for all later models.

Modek 3. We removed the time-signature dummy variables first because none were significant at α = 0.01. 

Multicollinearity Test: energy, loudness, and acousticness were highly correlated with each other (energy–loudness r = 0.76; energy–acousticness r = −0.72). 
We tested two branches — keeping energy and dropping loudness/acousticness (Model 4) versus dropping energy and keeping the other two (Models 5–7) — and selected **Model 4** as final. 

Final Model: Our final model has the better adjusted R² of models 4-7 (0.0728 vs. 0.0715 for the best alternative), we kept all predictors significant at α = 0.01, and reduced the collinearity concern by removing the two variables most entangled with energy. 

Interpretation: The final model explains only ~7.3% of the variation in popularity (danceability positive; energy, speechiness, instrumentalness, liveness, valence, tempo, and duration negative). 

## Interpretation and Conclusions 

Given the complexity of the music industry, audio features alone are a weak predictor of popularity — factors like artist recognition, marketing, and playlist placement are likely doing more of the work but aren't in this dataset. We suspected 'genre' to be a meaningful predictor as well, but dropped it due to having more categories than allowed.

Our dataset still shows interesting relationships between audio features and popularity. While we cannot assume causality, our dataset shows positive correlation of danceability on popularity, and negative correlations of mode, speechiness, instrumentalness, liveness, valence, tempo, explicit status, and duration. As an analyst and a heavy music listener, I believe these are meaningful relationships that reflect the tendencies (or nontendencies) of todays' songs that become ubiquitous.
