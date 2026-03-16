## Homework 4

Complete the following three questions in Python.  
These will be live coded and solved at the start of the following class.

Rules:
- Keep your code readable and use clear variable names.
- Use only `requests`, `pandas`, and `matplotlib` (plus Python built-ins).
- Print intermediate outputs so we can discuss your logic in class.

### Question 1: API pull + JSON parsing (health indicator)

Use the World Bank API to pull life expectancy (`SP.DYN.LE00.IN`) for these countries:

```python
countries = ["GBR", "USA", "BRA", "IND", "ZAF"]
```

Tasks:
1. For each country, send a GET request to `https://api.worldbank.org/v2/country/{country}/indicator/SP.DYN.LE00.IN` with params: `{"format": "json", "per_page": 100, "mrnev": 1}`.
2. Use `try/except` to handle bad status codes, bad JSON, and missing `value`.
3. Build `life_exp_records` with `country`, `year`, and `life_expectancy`, then convert it to a DataFrame.
4. Print the table sorted by `life_expectancy` (descending) and print the max-min gap.

### Question 2: Build a policy table with merges and derived metrics

You are given:

```python
import pandas as pd

health_df = pd.DataFrame({
    "area": ["Northside", "Central", "Riverside", "Eastbrook", "Hilltown"],
    "region_type": ["Urban", "Urban", "Rural", "Suburban", "Rural"],
    "clinic_visits": [1240, 980, 1430, 1110, 890],
    "school_absence_rate": [0.082, 0.051, 0.097, 0.064, 0.072],
    "population": [52000, 61000, 47000, 55000, 43000]
})

econ_df = pd.DataFrame({
    "area": ["Northside", "Central", "Riverside", "Eastbrook", "Hilltown"],
    "median_income": [29000, 37000, 25000, 33000, 27000],
    "unemployment_rate": [0.118, 0.074, 0.136, 0.091, 0.109],
    "public_health_budget": [2_400_000, 2_050_000, 2_650_000, 2_200_000, 1_950_000]
})
```

Tasks:
1. Merge the two DataFrames into `policy_df` on `area`.
2. Create these columns:
   - `visits_per_1000` = `clinic_visits / population * 1000`
   - `budget_per_visit` = `public_health_budget / clinic_visits`
   - `stress_index` = `school_absence_rate * unemployment_rate * 1000`
3. Print the top 2 areas by `stress_index`.
4. Group by `region_type` and print the mean values of:
   - `visits_per_1000`
   - `median_income`
   - `unemployment_rate`

### Question 3: Communicate inequality and risk with one figure

Using `policy_df` from Question 2, build one matplotlib figure with 3 subplots (`1x3`):

1. A bar chart of `visits_per_1000` by `area`.
2. A scatter chart:
   - x = `unemployment_rate`
   - y = `school_absence_rate`
   - marker size = `public_health_budget / 50000`
   - annotate each point with `area`
3. A histogram of `median_income`.

Requirements:
- Use clear titles and axis labels.
- Add a grid where appropriate.
- Call `plt.tight_layout()`.
- Save the figure to `../Figures/homework_4_policy_dashboard.png`.

Stretch (optional):
- Print one short line identifying one high-risk area and why.