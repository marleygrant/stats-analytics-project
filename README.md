# stats-analytics-project
# Predictors of Team Success — EPL & Serie A Player Statistics

**One-line description:** A regression-based analysis of which individual player performance
metrics are associated with team-level success (points per match) across 1,074 EPL and Serie A
players.

A semester-long analytics project (BAN 6001) applying descriptive statistics, probability,
distribution analysis, hypothesis testing, and regression modeling to a 1,074-player dataset
from the English Premier League and Italian Serie A.

## Dataset

- **Source:** Combined player-level statistics for the 2023–24 EPL and Serie A seasons
  (standard stats + playing-time tables merged on player ID and squad).
- **Size:** 1,074 players after merging (from a raw pool of 1,160 — records that didn't
  appear in both source tables were dropped).
- **Topic:** Individual player performance metrics (minutes played, goal involvement,
  discipline, position, nationality) against team-level success.
- **Research question:** Which player performance and squad-role metrics are associated with
  a player's team's points-per-match — and how much of that variation can a linear model
  actually explain?

> **Note on Assignment 2:** Assignment 2 was completed on a different dataset (an e-commerce
> sales dataset from Kaggle, focused on Revenue) with a different project team (Ragan Price,
> D'Marley Grant, Simon Malone). Starting with Assignment 3, the project shifted to the
> EPL/Serie A player statistics dataset used through Assignment 6. Both are included here for
> a complete record of the coursework.

## Repository Structure

```
README.md                          This file
DECISIONS.md                       Dated log of the analytical choices behind each assignment
data/                               Raw dataset from Assignment 2 (e-commerce, Kaggle)
assignment-02-dataset/             Variable selection & project proposal (Word doc)
assignment-03-descriptive-stats/   Frequency tables & summary stats by variable
assignment-04-probability/         Distribution analysis — empirical vs. theoretical comparisons
assignment-05-inference/           Hypothesis testing & confidence intervals
assignment-06-regression/          Multiple regression — backward elimination to a final model
```

## Author

D'Marley Grant — MSBA Candidate, Wake Forest University School of Business.
Assignments 2–6 were completed as part of a team project; this repository reflects
individual submission of the team's shared analytical work, per course requirements.
