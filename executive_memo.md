# Lab | Week 7 | Day 5 | In God we trust, everyone else bring the data
## John Adams

## Header

**Title:** Marketing Channel Performance Review and Budget Allocation Recommendation
**Date:** 2026-08-24
**Analyst:** John Adams
**Dataset used:** Global Ads Performance (Google, Meta, TikTok), Kaggle
**Period analyzed:** 2024-01-01 to 2024-12-30 (daily data, 3 platforms)

## Executive Summary

We compared cost per acquisition (CPA), return on ad spend (ROAS), and conversion rate across our three paid channels: Google Ads, Meta Ads, and TikTok Ads. TikTok Ads has the lowest CPA and the highest ROAS of the three, and the gap is both statistically significant and large enough to matter for budget planning. Conversion rate also differs significantly between channels, but the actual gaps are tiny (0.12-0.24 percentage points) and should not drive budget decisions on their own. We recommend shifting the composite-score-weighted majority of the $500K monthly budget toward TikTok Ads and Meta Ads, while reducing Google Ads' share, subject to the caveats below.

## Key Findings

**Top performing channel:** TikTok Ads. Lowest CPA ($29.20 average), highest ROAS (9.54x average).
**Lowest performing channel:** Google Ads. Highest CPA ($64.06 average), lowest ROAS (4.11x average).
**Middle:** Meta Ads (CPA $39.10, ROAS 6.92x).

**Statistically significant differences found (after Benjamini-Hochberg FDR correction, alpha=0.05):**
- Meta Ads has lower CPA than Google Ads by $24.97 (FDR p=3.4e-26, Cohen's d=-0.60, medium effect)
- TikTok Ads has lower CPA than Google Ads by $34.87 (FDR p=1.0e-39, Cohen's d=-0.88, large effect)
- TikTok Ads has lower CPA than Meta Ads by $9.90 (FDR p=2.0e-08, Cohen's d=-0.35, small effect)
- TikTok Ads has a higher conversion rate than Google Ads by 0.24 percentage points (FDR p=1.6e-42), but this is not a practically meaningful gap
- All 9 comparisons run (6 t-tests, 3 Fisher's exact tests) remained significant under both Bonferroni and FDR correction; none of our findings were false positives from running many tests

**Data adequacy (power analysis):** With 90 days of daily data, we have essentially 100% power to detect the CPA differences we actually observed (34% to 119% relative gaps), since these are far larger than the 10-20% effect sizes our simulations show are reliably detectable at that sample size. A much smaller difference, around 5%, would need roughly 180 days of data to detect reliably at 90 days we would only catch it about 60% of the time. This is not a concern for the findings above, but is worth knowing before running smaller, more subtle future tests.

## Recommendations

**Budget allocation:** Reallocate the $500K monthly budget using a composite score based on CPA and ROAS (weighted 50/50), with a floor of 15% and a ceiling of 55% per channel so no channel is starved or given the entire budget.

| Platform | Composite score (lower is better) | Allocation % | Allocation amount |
|---|---|---|---|
| TikTok Ads | 1.0 | 50% | $250,000 |
| Meta Ads | 2.0 | 33% | $166,667 |
| Google Ads | 3.0 | 17% | $83,333 |

Full calculation in `statistical_analysis.ipynb` (Part 5, Step 8).

**Strategic actions:**
- Increase TikTok Ads spend, it has the strongest cost efficiency and return, with a large, well-supported effect size.
- Maintain or modestly increase Meta Ads spend, it is a solid middle performer, statistically distinct from both other channels.
- Reduce Google Ads spend relative to the other two channels, but do not eliminate it. The 15% floor keeps a foothold in case of channel-specific risk (platform policy changes, audience saturation elsewhere) and Google Ads may serve roles beyond pure CPA/ROAS (e.g. brand search coverage) not captured in this dataset.
- Do not use conversion rate as a channel-selection lever. The differences are statistically real but too small (fractions of a percentage point) to justify budget shifts on their own.

## Next Steps

- Validate this dataset's pattern against our own first-party campaign data before shifting real budget.
- Re-run this comparison quarterly as new data comes in, since channel performance can shift with market conditions.
- If testing smaller optimizations in the future (e.g. a 5-10% CPA improvement from a creative change), budget for a longer test window (60-180 days) based on the power analysis above.
- Investigate whether Google Ads serves a strategic role (brand search, upper-funnel awareness) not captured by CPA/ROAS alone, before reducing its budget share too aggressively.

## Appendix: Statistical Caveats

**Dataset limitations and source:** This analysis uses a Kaggle dataset ("Global Ads Performance: Google, Meta, TikTok") covering 2024 daily campaign performance. It is a third-party dataset, not our company's own campaign data. Before acting on these findings with real budget, validate the pattern against our own attribution and spend data.

**Multiple comparisons correction applied:** With 9 total comparisons run, we expected roughly 0.45 false positives by chance alone at alpha=0.05. We applied both Bonferroni (strict) and Benjamini-Hochberg FDR (moderate) corrections; all 9 results survived both, meaning none of our conclusions are likely artifacts of running many tests.

**Confidence intervals:** 95% bootstrap confidence intervals for CPA do not overlap between any pair of channels (Google $60.52-$67.55, Meta $36.82-$41.58, TikTok $26.99-$31.69), reinforcing that these are real, distinguishable differences, not noise.

**External factors:** This dataset does not capture seasonality drivers, competitor activity, creative quality, audience targeting changes, or platform algorithm updates over the year, any of which could shift future performance independent of the channel itself.

**Statistical vs. practical significance:** All 9 tests were statistically significant, but the conversion rate differences (0.12-0.24 percentage points) are not practically meaningful at this sample size, while the CPA and ROAS differences (25-132% relative gaps, medium to large Cohen's d) are both statistically and practically significant. Budget decisions should weight the latter, not the former.

**Power analysis limitations:** Our power simulations assumed CPA is roughly normally distributed with 15% day-to-day variability, based on the observed data. Future channels, campaigns, or market conditions may not follow the same variability pattern, and this simulation should be re-run periodically rather than treated as a fixed rule.
