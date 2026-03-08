## Homework 3 (Live-Coding Prep)

Complete the following three questions in Python.  
These will be live coded and solved at the start of the following class.

Rules:
- Use clear variable names and readable NumPy code.
- Use only `numpy` (plus Python built-ins).
- Print intermediate outputs so we can discuss your logic in class.

### Question 1: Income inequality with NumPy (Gini coefficient)

You are given:

```python
import numpy as np

incomes_a = np.array([12000, 18000, 22000, 26000, 34000, 85000])
incomes_b = np.array([22000, 24000, 25000, 26000, 27000, 29000])
```

Tasks:
1. Write a NumPy function `gini(x)` that returns the Gini coefficient for a 1D income array.
2. Compute and print `gini(incomes_a)` and `gini(incomes_b)`.
3. Print which group is more unequal.
4. For each group, also print mean and median income.

### Question 2: Health economic cost function (vectorized)

You are given:

```python
age = np.array([35, 52, 47, 61, 29, 44])
chronic_conditions = np.array([0, 2, 1, 3, 0, 1])
emergency_visits = np.array([1, 0, 2, 3, 1, 2])
```

Use this cost function:

`cost = 450 + 120*age + 1500*chronic_conditions + 900*emergency_visits`

Tasks:
1. Compute and print the vector of individual costs.
2. Print mean cost and total cost.
3. Recompute costs under a policy scenario where emergency visits fall by 20%.
4. Print the average cost saving per person.

### Question 3: Random shocks and risk probabilities

Set a random seed and generate 1,000 income shocks from a normal distribution:

```python
mean = 0
sd = 1500
```

Tasks:
1. Print the first 5 draws.
2. Print the share of draws below `-2000`.
3. Print the share of draws above `+2000`.
4. Create a NumPy label array with:
   - `"severe_negative"` if shock < -2000
   - `"stable"` if -2000 <= shock <= 2000
   - `"severe_positive"` if shock > 2000
5. Print the count in each label group.

Stretch (optional):
- Change `sd` from `1500` to `2200`, rerun, and print how the severe-negative share changes.
