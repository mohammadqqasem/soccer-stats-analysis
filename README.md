# Does Possession Win Matches? A Study of the Top 5 European Leagues (2008–2016)

## 1. Research Question

Does the team with more possession in a match win more often across the top 5 European leagues — and did possession-based football grow in influence between 2008 and 2016?

This question matters because possession is one of the most debated statistics in football. The rise of Pep Guardiola's Barcelona (2008–2012) convinced much of the football world that dominating the ball was the path to winning. But as counter-pressing tactics emerged — most notably under Jürgen Klopp at Borussia Dortmund — that assumption was increasingly challenged. This project uses match data to test whether the numbers actually support the possession-wins narrative, and whether the answer differs across Europe's top leagues.

## 2. Hypothesis

**Main Hypothesis:**  
- Null: There is no difference in win rate between the team with more possession and the team with less possession — any observed difference is due to chance.  
- Alternative: The team with higher possession wins significantly more often than the team with lower possession across the top 5 European leagues.

**Trend Hypothesis:**  
- Null: There is no difference in average possession patterns between the early era (2008–2012) and the late era (2012–2016).  
- Alternative: Possession patterns shifted significantly across the two eras, reflecting the tactical evolution from tiki-taka to counter-pressing.

## 3. Data Description

- **Source:** [European Soccer Database](https://www.kaggle.com/datasets/hugomathien/soccer) — Kaggle (CC0 Public Domain), originally sourced from football-data.org
- **Unit of analysis:** One row = one match
- **Matches:** ~14,000 matches with valid possession data (out of 25,979 total)
- **Seasons:** 2008/2009 through 2015/2016 (8 seasons)
- **Leagues:** Premier League (England), La Liga (Spain), Bundesliga (Germany), Serie A (Italy), Ligue 1 (France)

**Key variables:**
| Variable | Description |
|----------|-------------|
| `home_poss` | Home team final possession percentage |
| `away_poss` | Away team final possession percentage |
| `home_team_goal` | Goals scored by home team |
| `away_team_goal` | Goals scored by away team |
| `result` | Match result: Home Win, Away Win, or Draw |
| `poss_team_won` | Whether the team with more possession won (True/False) |
| `league` | League name |
| `season` | Season (e.g. 2008/2009) |

**Cleaning steps:**
- Possession values were stored as XML in the database and parsed to extract final match possession figures
- Matches where both teams had equal possession were excluded
- Matches with missing or unparseable possession data were dropped
- Analysis filtered to top 5 leagues only (league IDs: 1729, 4769, 7809, 10257, 21518)

**Data file:** The `database.sqlite` file is not committed to this repo due to its size. 

## 4. Methods

**Permutation Test (Main Hypothesis):**
- Test statistic: Win rate of the team with more possession
- Null simulation: Shuffled the `poss_team_won` column 10,000 times and recomputed win rate each time
- P-value: Proportion of permuted win rates ≥ observed win rate

**Permutation Test (Trend Hypothesis):**
- Test statistic: Difference in mean possession between early era (2008–2012) and late era (2012–2016)
- Null simulation: Randomly shuffled era labels 10,000 times

**Bootstrap Confidence Intervals:**
- Metric 1: Overall win rate (proportion) — CLT applies but bootstrapped for consistency (10,000 resamples)
- Metric 2: Median possession of winning teams by league — **CLT does not apply** to medians because the sampling distribution of the median depends on the density at the population median, not just the variance. Bootstrapping is the appropriate method here (10,000 resamples, 95% confidence intervals)

## 5. Results

- The team with more possession won significantly more often than chance (50%) across all top 5 leagues
- The permutation test confirmed this result is statistically significant (p < 0.05)
- La Liga showed the strongest possession-win relationship, consistent with its tiki-taka culture
- The Premier League and Serie A showed weaker relationships, reflecting counter-attacking and defensive traditions respectively
- Possession patterns shifted between the early and late eras, capturing the tactical evolution of European football


## 6. Uncertainty Estimation

- 10,000 bootstrap resamples were used for all confidence intervals
- Bootstrap distributions were approximately normal for the win rate metric
- For league-level median possession, bootstrap distributions showed varying spread, with La Liga and Bundesliga showing tighter intervals (more consistent patterns) than Ligue 1
- All 95% confidence intervals for win rate excluded 50%, confirming the effect is consistent across resamples

## 7. Limitations

- Possession data is only available for approximately 55% of matches in the dataset, which may introduce selection bias if missing data is not random
- The dataset ends in 2016 and does not capture more recent tactical trends (e.g. high press, low-block defending)
- Possession is measured as a final match figure, which can be inflated when a winning team sits back and the losing team chases the game — this introduces reverse causality
- The analysis does not control for team quality, opponent strength, or match context (e.g. score at half time)
- Ligue 1 has historically had lower data quality and fewer matches with possession data recorded

## 8. References

- Mathien, H. (2016). *European Soccer Database*. Kaggle. https://www.kaggle.com/datasets/hugomathien/soccer
- Data originally sourced from football-data.org API
- Python libraries used: `pandas`, `numpy`, `matplotlib`, `seaborn`, `sqlite3`, `xml.etree.ElementTree`

---

**Repository Structure:**
```
soccer-stats-analysis/
├── data/               # Place database.sqlite here (not committed)
├── results/            # Generated figures saved here
├── analysis.ipynb      # Main analysis notebook
└── README.md           # This file
```
