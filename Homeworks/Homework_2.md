## Homework 2

Complete the following three questions in Python.  
These will be live coded and solved at the start of the following class.

Rules:
- Keep your code readable and use clear variable names.
- Do not import external libraries.
- Print intermediate outputs so we can discuss your logic in class.

### Question 1: Risk Flagging with Loop + If/Elif

You are given:

```python
area_records = [
    {"area": "Northside", "clinic_visits": 120, "school_absence_rate": 0.07, "median_income": 29000},
    {"area": "Central", "clinic_visits": 95, "school_absence_rate": 0.05, "median_income": 36000},
    {"area": "Riverside", "clinic_visits": 140, "school_absence_rate": 0.09, "median_income": 25000}
]
```

Tasks:
1. Loop through each area record.
2. Print `high risk` if `school_absence_rate > 0.08` OR `median_income < 27000`.
3. Print `moderate risk` if `clinic_visits > 110` and the area is not already high risk.
4. Otherwise print `lower risk`.
5. Print the area name and label on one line each.

### Question 2: Build a Nested Dictionary with zip

You are given:

```python
areas = ["Northside", "Central", "Riverside"]
clinic_visits = [120, 95, 140]
unemployment_rate = [0.12, 0.08, 0.15]
rent_burden = [0.31, 0.26, 0.37]
```

Tasks:
1. Use `zip` to build a nested dictionary called `area_metrics` where each area maps to:
   - `clinic_visits`
   - `unemployment_rate`
   - `rent_burden`
2. Print `area_metrics["Central"]`.
3. Compute and print the area with the highest unemployment rate.
4. Compute and print average clinic visits using values pulled from `area_metrics` (no hard-coded numbers).

### Question 3: Error Handling in Data Cleaning

You are given:

```python
raw_visits = ["120", "95", "missing", "140", "n/a", "102"]
```

Tasks:
1. Loop through `raw_visits`.
2. Use `try/except` to convert valid values to integers and append to `clean_visits`.
3. Append invalid entries to `invalid_entries`.
4. Print both lists.
5. Print the mean of `clean_visits` using `sum(clean_visits) / len(clean_visits)`.

Stretch (optional, still no imports):
- Print invalid values as one comma-separated string using `", ".join(...)`.