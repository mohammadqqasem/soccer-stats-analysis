# Did COVID Kill Home Advantage? A Study of the Top 5 European Leagues

## 1. Research Question

Did home advantage disappear during the COVID season when stadiums were empty, and did it recover once fans returned?

Home advantage is one of the most debated topics in football — teams consistently win more at home than away. But during the 2019/20 season, matches were played behind closed doors with no fans due to COVID-19. This created a unique natural experiment: what actually happens to home advantage when you remove the crowd?

## 2. Hypothesis

**Null Hypothesis:** There is no difference in home win rates across the three seasons — any observed differences are due to chance.

**Alternative Hypothesis:** Home win rates dropped significantly during the COVID season (2019/20) compared to the last normal season (2018/19), and recovered in the first season fans returned (2020/21).

## 3. Data Description

- **Source:** Club Football Match Data (2000–2025) — [GitHub](https://github.com/xgabora/Club-Football-Match-Data-2000-2025)
- **Unit of analysis:** One row = one match
- **Leagues:** Premier League (E0), La Liga (SP1), Bundesliga (D1), Serie A (I1), Ligue 1 (F1)
- **Seasons compared:**
  - 2018/19 — Last normal season (fans present) — 1,826 matches
  - 2019/20 — COVID season (no fans) — 1,715 matches
  - 2020/21 — First season back (fans returned) — 1,836 matches

**Key variables:**

| Variable | Description |
|----------|-------------|
| `FTResult` | Full-time result: H = Home Win, D = Draw, A = Away Win |
| `Division` | League code (E0, SP1, D1, I1, F1) |
| `MatchDate` | Date of the match |

**Cleaning steps:**
- Filtered to top 5 European leagues only
- Converted `MatchDate` to datetime
- Split data into three seasons using date ranges
- Dropped rows with missing `FTResult`

**Data file:** `Matches.csv` — place in the same folder as the notebook to run the analysis. Download from the source link above.

## 4. Methods

*(To be completed in final submission)*

- **Permutation test:** Compare home win rates between the pre-COVID and COVID seasons by shuffling season labels 10,000 times
- **Bootstrap confidence intervals:** Estimate uncertainty around the home win rate for each season
- **Non-CLT metric:** Median goal difference in home wins — bootstrapping will be used since CLT does not apply to medians

## 5. Results

**Home win rates across the three seasons:**

| Season | Matches | Home Wins | Draws | Away Wins |
|--------|---------|-----------|-------|-----------|
| 2018/19 (Pre-COVID) | 1,826 | 817 (44.7%) | 472 (25.8%) | 537 (29.4%) |
| 2019/20 (COVID) | 1,715 | 758 (44.2%) | 418 (24.4%) | 539 (31.4%) |
| 2020/21 (Post-COVID) | 1,836 | 731 (39.8%) | 467 (25.4%) | 638 (34.7%) |

**Key finding:** Surprisingly, the COVID season barely affected the home win rate (44.7% → 44.2%). The bigger drop came in the first season fans returned (39.8%), when away wins jumped from 29.4% to 34.7%. This challenges the assumption that empty stadiums hurt home teams the most and suggests something more complex is happening.

## 6. Uncertainty Estimation

*(To be completed in final submission)*

## 7. Limitations

- The 2019/20 season was disrupted mid-season by COVID — some early matches had fans present before lockdowns
- The 2020/21 season had partial fan attendance in some leagues as restrictions varied by country
- The analysis does not control for team quality, transfers, or other factors that changed between seasons
- Only three seasons are compared — a longer trend analysis would give more context

## 8. References

- Gábor, A. (2025). *Club Football Match Data*. Retrieved from https://github.com/xgabora/Club-Football-Match-Data-2000-2025
- Python libraries used: `pandas`, `numpy`, `matplotlib`


