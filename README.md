# Did COVID Kill Home Advantage? A Study of the Top 5 European Leagues

## 1. Research Question

Did home advantage disappear during the COVID season when stadiums were empty, and did it recover once fans returned?

Home advantage is one of the most debated topics in football — teams consistently win more at home than away. But during the 2019/20 season, matches were played behind closed doors with no fans due to COVID-19. This created a unique natural experiment: what actually happens to home advantage when you remove the crowd? And did things go back to normal once fans returned?

**Important note:** Fans were not truly back until the 2021/22 season. The 2020/21 season was almost entirely played behind closed doors — only the final 1-2 home games allowed limited capacity (up to 10,000 or 25%). Full stadiums only returned in August 2021.

## 2. Hypothesis

**Null Hypothesis:** There is no difference in home win rates across the four seasons — any observed differences are due to chance.

**Alternative Hypothesis:** Home win rates dropped during the fanless seasons and recovered when fans fully returned in 2021/22.

## 3. Data Description

- **Source:** Club Football Match Data (2000–2025) — [GitHub](https://github.com/xgabora/Club-Football-Match-Data-2000-2025)
- **Unit of analysis:** One row = one match
- **Leagues:** Premier League (E0), La Liga (SP1), Bundesliga (D1), Serie A (I1), Ligue 1 (F1)
- **Seasons compared:**
  - 2018/19 — Last normal season (fans present) — 1,826 matches
  - 2019/20 — COVID season (no fans) — 1,715 matches
  - 2020/21 — Still mostly no fans (limited capacity last 1-2 games only) — 1,836 matches
  - 2021/22 — First full-capacity season since COVID — 1,826 matches

**Key variables:**

| Variable | Description |
|----------|-------------|
| `FTResult` | Full-time result: H = Home Win, D = Draw, A = Away Win |
| `Division` | League code (E0, SP1, D1, I1, F1) |
| `MatchDate` | Date of the match |
| `FTHome` / `FTAway` | Goals scored by home and away teams |

**Cleaning steps:**
- Filtered to top 5 European leagues only
- Converted MatchDate to datetime
- Split data into four seasons based on date ranges
- Dropped rows with missing FTResult

**Data file:** Place `Matches.csv` in the same folder as the notebook. Download from the source link above.

## 4. Methods

**Three Permutation Tests (10,000 shuffles each):**
- Test 1: Pre-COVID vs 2020/21 (no fans) — was the drop significant?
- Test 2: 2020/21 vs 2021/22 — was the recovery significant?
- Test 3: Pre-COVID vs 2021/22 (fans back) — is the fans-back season statistically different from pre-COVID?

For each test: pool both seasons, shuffle the labels 10,000 times, recompute the difference each time, and report the p-value.

**Bootstrap Confidence Intervals:**
- Metric 1: Home win rate per season — resampled 10,000 times for a 95% CI per season
- Metric 2: Median goal difference in home wins — CLT does not apply to medians, so bootstrapping is used

## 5. Results

**Home win rates across all four seasons:**

| Season | Fans? | Matches | Home Wins | Draws | Away Wins |
|--------|-------|---------|-----------|-------|-----------|
| 2018/19 (Pre-COVID) | ✅ Full | 1,826 | 817 (44.7%) | 472 (25.8%) | 537 (29.4%) |
| 2019/20 (COVID) | ❌ None | 1,715 | 758 (44.2%) | 418 (24.4%) | 539 (31.4%) |
| 2020/21 (Still no fans) | ❌ Barely | 1,836 | 731 (39.8%) | 467 (25.4%) | 638 (34.7%) |
| 2021/22 (Fans fully back) | ✅ Full | 1,826 | 781 (42.8%) | 471 (25.8%) | 574 (31.4%) |

**Permutation test results:**

| Comparison | Difference | P-value | Conclusion |
|-----------|-----------|---------|------------|
| Pre-COVID vs 2020/21 (no fans) | 4.93% | 0.0019 | Significant drop ✅ |
| 2020/21 vs 2021/22 (recovery) | 2.96% | 0.074 | Not significant |
| Pre-COVID vs 2021/22 (fans back) | 1.97% | 0.2524 | Not significant — home advantage restored ✅ |

**Key finding:** Crowds genuinely matter. The fanless 2020/21 season caused a statistically significant drop in home advantage. When fans fully returned in 2021/22, the home win rate was no longer statistically different from pre-COVID — home advantage was essentially restored.

**Bootstrap CIs (home win rate):**
- 2018/19: 44.7% | CI: [42.4%, 47.0%]
- 2019/20: 44.2% | CI: [41.8%, 46.6%]
- 2020/21: 39.8% | CI: [37.6%, 42.0%]
- 2021/22: 42.8% | CI: [40.6%, 45.0%]

**Median goal difference in home wins:** 2.0 across all four seasons — COVID changed how often home teams won, not by how much.

## 6. Uncertainty Estimation

- Used 10,000 resamples for all permutation tests and bootstrap intervals
- The Pre-COVID and Fans Back bootstrap distributions overlap significantly, consistent with the permutation test finding that they are not statistically different
- The 2020/21 distribution is clearly shifted lower and barely overlaps with the others
- All findings are consistent across resamples

## 7. Limitations

- The 2019/20 season started with fans before COVID hit mid-season — it is not a clean no-fans season from the start
- The 2020/21 season had limited fans (up to 10,000 or 25% capacity) for the final 1-2 games
- The analysis does not control for team quality, transfers, or other factors that changed between seasons
- Only four seasons are compared — a longer trend analysis would give more context
- Other European leagues had different fan restriction timelines, which may affect the cross-league comparison

## 8. References

- Gábor, A. (2025). *Club Football Match Data*. Retrieved from https://github.com/xgabora/Club-Football-Match-Data-2000-2025
- Python libraries used: `pandas`, `numpy`, `matplotlib`


```
