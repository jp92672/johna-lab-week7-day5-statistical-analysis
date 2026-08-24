# Lab | Week 7 | Day 5 | In God we trust, everyone else bring the data
## John Adams

## How to run

1. Install dependencies: `numpy`, `pandas`, `matplotlib`, `seaborn`, `scipy` (1.11+), `jupyter`.
2. Run `data_exploration.ipynb` first, it loads the raw dataset, cleans it, and saves `Data/marketing_data.csv`.
3. Run `statistical_analysis.ipynb` next, it reads `Data/marketing_data.csv` and depends on Step 2's output existing.

## File map

- `data_exploration.ipynb` — Part 1: loads and cleans the raw dataset, calculates key marketing metrics, saves `Data/marketing_data.csv`
- `statistical_analysis.ipynb` — Parts 2-5: t-tests, Fisher's exact tests, multiple comparisons correction, power analysis, and business recommendations
- `lab_summary.md` — dataset choice documentation and key insights from Part 1
- `executive_memo.md` — final business memo with findings, budget allocation, and statistical caveats
- `Data/raw_global_ads_performance.csv` — raw dataset as downloaded from Kaggle
- `Data/marketing_data.csv` — cleaned dataset used by all analysis steps
- `Outputs/` — all saved chart images referenced in the notebooks and memo

## Setup assumptions

- Dataset: Global Ads Performance (Google, Meta, TikTok), Kaggle, https://www.kaggle.com/datasets/nudratabbas/global-ads-performance-google-meta-tiktok
- Grouping variable: `platform` (Google Ads, Meta Ads, TikTok Ads)
- `data_exploration.ipynb` must be run before `statistical_analysis.ipynb`, since the second notebook reads the CSV the first one produces.

## Submission hygiene

- Keep this repository scoped to this lab only — no unrelated projects or personal files.
- Use clear, descriptive filenames.
- Remove secrets, API keys, and tokens before committing.
