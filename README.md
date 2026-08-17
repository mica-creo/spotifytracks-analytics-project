# Spotify Track Popularity Analysis
Which audio characteristics contribute to a song's popularity? My team and I conducted a multiple regression of a Kaggle-sourced dataset of around 90,000 Spotify tracks.

## Dataset

- **Source:** [Spotify Tracks Dataset](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset) by Maharshi Pandya, hosted on Kaggle ([DOI](https://doi.org/10.34740/kaggle/dsv/4372070)). Downloaded manually as a CSV via the Kaggle site.
- **Topic:** Spotify song characteristics (danceability, energy, loudness, tempo, etc.) and their relationship to popularity.
- **Size:** ~114,000 raw tracks; 89,740 unique tracks after removing duplicate `track_id` values. 13 analytical variables (11 continuous, 2 categorical).
- **Main research question:** Which audio characteristics are associated with higher song popularity on Spotify?

## What's in this repo

| Folder | Contents |
|---|---|
| `Assignment 2 - Dataset Selection` | Our selected Dataset including cleaned version, project information, main variables of interest, and requirements check |
| `Assignment 3 - Descriptive Statistics and Data Visualization` | Exploring the variables of our dataset with frequency tables, and their distributions through visuals like histograms:  |
| `Assignment 4 - Probability and Distribution` | Summary statistics for each variable, assessment of their distribution, and probabilities of certain values within variables.  |
| `Assignment 5 - Hypothesis Testing and Confidence Intervals` | Hypothesis tests and a confidence interval for popularity/danceability |
| `Assignment 6 - Regression Analysis` | Multiple regression models refitted to assure significance, accurate variable relationships, and multicollinearity diagnostics. Final model selection and commentary |

See `DECISIONS.md` for the reasoning behind the key analytical choices made at each stage.

## About

By Micaela Creo. This analysis was completed as a team with Scott Robinson and Ming Chen as coursework for the MSBA program.

