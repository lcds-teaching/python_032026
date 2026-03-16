## Homework 1

Complete the following three questions in Python.  
These will be live coded and solved at the start of the following class.

Rules:
- Keep your code readable and use clear variable names.
- Do not import external libraries.
- Print intermediate outputs so we can discuss your logic in class.

### Question 1: Parse one semi-structured record

You are given:

```python
record = "northside|clinic_visits=120|school_absence_rate=0.07|median_income=29000"
```

Tasks:
1. Split the string into parts.
2. Build a dictionary called `northside_record` with keys:
   - `area` (as a string in title case, e.g. `"Northside"`)
   - `clinic_visits` (as `int`)
   - `school_absence_rate` (as `float`)
   - `median_income` (as `int`)
3. Print a summary sentence using an f-string:
   - Example structure: `"Northside had 120 clinic visits, 7.0% absence, median income 29000."`

### Question 2: Build a nested data structure from parallel lists

You are given:

```python
areas = ["Northside", "Central", "Riverside"]
clinic_visits = [120, 95, 140]
school_absence_rate = [0.07, 0.05, 0.09]
median_income = [29000, 36000, 25000]
```

Tasks:
1. Build a nested dictionary called `area_data` with this structure:
   - top-level keys are area names
   - values are dictionaries with keys `clinic_visits`, `school_absence_rate`, `median_income`
2. Print the value of `area_data["Central"]["median_income"]`.
3. Compute and print the clinic-visit gap between Riverside and Central.
4. Compute and print the area name with the highest median income.

Constraint:
- After creating `area_data`, do not hard-code numeric values in your calculations.

### Question 3: Clean and deduplicate messy indicator names

You are given:

```python
raw_indicators = [
    " Clinic_Visits ",
    "school_absence_rate",
    "MEDIAN_INCOME",
    "clinic_visits",
    " School_Absence_Rate ",
    "median_income "
]
```

Tasks:
1. Create a cleaned list called `clean_indicators` where each value is:
   - lower case
   - stripped of surrounding whitespace
2. Create a set called `unique_indicators` from `clean_indicators`.
3. Print:
   - `clean_indicators`
   - `unique_indicators`
   - the number of raw indicators
   - the number of unique indicators
4. Print whether `"clinic_visits"` and `"median_income"` are in `unique_indicators`.

Stretch (optional, still no imports):
- Create a sorted list from `unique_indicators` and print it.