# Lab | Week 7 | Day 5 | In God we trust, everyone else bring the data
## John Adams

## Part 1: Dataset Discovery & Exploration
### Step 1: Find and Select a Dataset

**Dataset:** Global Ads Performance (Google, Meta, TikTok)
**Source:** Kaggle, https://www.kaggle.com/datasets/nudratabbas/global-ads-performance-google-meta-tiktok
**Why chosen:** 1,800 daily campaign rows across three ad platforms (Google Ads, Meta Ads, TikTok Ads), no missing values, full 2024 date range. Already includes every metric named in this lab's instructions (impressions, clicks, CTR, ad_spend, conversions, CPA, revenue, ROAS), and the fields correlate with each other the way real ad performance data should (clicks track impressions, revenue tracks conversions, CPA and ROAS move opposite each other). A separate synthetic lead-scoring dataset and a synthetic 200K-row campaign dataset were checked first; both had numeric columns with ~0.000 correlation to each other and near-identical channel means, meaning no real signal to detect. This dataset does not have that problem.

**Grouping variable:** `platform` (Google Ads, Meta Ads, TikTok Ads) — 3 groups, meets the lab's minimum.
**Secondary dimensions available but not used as the primary group:** `campaign_type`, `industry`, `country`.

### Step 2: Load and Explore Your Dataset

**Transformations applied:** parsed `date` to datetime; recomputed CTR, CPA, and ROAS directly from base counts (impressions, clicks, ad_spend, conversions, revenue) rather than trusting the source's precomputed columns, then confirmed they matched; replaced division-by-zero results (inf) with NaN; added `conversion_rate`, `profit`, and `profit_margin`.

### Step 2: Calculate Key Marketing Metrics

**Key insights:**
- TikTok Ads has the lowest CPA and highest ROAS of the three platforms; Google Ads has the highest CPA and lowest ROAS.
- CPA and ROAS both show wide day-to-day spread within each platform (visible in the box plots), so the group-level averages above should not be read as fixed constants. Statistical testing in the next notebook checks whether the platform differences are larger than that day-to-day noise.
- No platform shows an obvious outlier day (e.g. spend or conversions clearly detached from the rest of that platform's distribution).
