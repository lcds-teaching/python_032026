# Good Research Practice with Python for Statistical Analysis

## Audience and goal

This note is for students learning Python mainly for data and statistical analysis.
The target is not "production software", but reliable research code that other people can rerun.

Good engineering habits make your analysis:

- reproducible
- easier to mark and review
- easier to debug
- safer to extend for reports, thesis work, or papers

## A clear baseline project structure

Use separate folders for data, figures, and source code from day one.

```text
project/
  data/
    raw/
    processed/
  figs/
  src/
    params.py
    io_utils.py
    cleaning.py
    stats_models.py
    plotting.py
    run_analysis.py
  notebooks/
    01_exploration.ipynb
    02_checks.ipynb
  tests/
    test_cleaning.py
  requirements.txt
  README.md
```

Why this helps:

- `data/raw` is immutable input
- `data/processed` stores transformed data
- `figs` centralizes output graphics
- `src` contains reusable code (not mixed with notebook scratch work)

## 1) Put parameters that you are going to reuse in one place (for example, a separate file)

### Bad

```python
# values scattered across files and cells
ALPHA = 0.05
SEED = 1
TEST_SIZE = 0.3
```

### Good

```python
# src/params.py
from dataclasses import dataclass

alpha = 0.05
seed = 2026
test_size = 0.2
outcome_col = "y"
```

```python
# src/run_analysis.py
import params 

alpha = params.alpha
```

Why this helps:

- one edit point for experimental settings
- fewer mistakes when rerunning with changed assumptions
- easy to report exact setup in methods sections

## 2) Avoid hidden global state

### Bad

```python
THRESHOLD = 10


def flag_high_risk(df):
    return df["score"] > THRESHOLD
```

### Good

```python
def flag_high_risk(df, threshold):
    return df["score"] > threshold
```

```python
from params import Params

params = Params()
df["high_risk"] = flag_high_risk(df, threshold=10)
```

Guideline: functions should receive what they need as arguments.

## 3) Separate analysis steps into functions

### Bad

```python
# one long script cell mixing loading, cleaning, modeling, plotting
import pandas as pd
from sklearn.linear_model import LogisticRegression
df = pd.read_csv("data/raw/patients.csv")
df = df.dropna()
X = df[["age", "bmi"]]
y = df["outcome"]
model = LogisticRegression().fit(X, y)
print(model.score(X, y))
```

### Good

```python
def load_data(path):
    import pandas as pd
    return pd.read_csv(path)


def clean_data(df):
    return df.dropna(subset=["age", "bmi", "outcome"])


def fit_model(df):
    from sklearn.linear_model import LogisticRegression
    X = df[["age", "bmi"]]
    y = df["outcome"]
    return LogisticRegression(max_iter=1000).fit(X, y)
```

This split makes testing and error isolation much easier.

## 4) Make randomness reproducible

### Bad

```python
import numpy as np
boot = np.random.choice(values, size=(1000, len(values)), replace=True)
```

### Good

```python
import numpy as np


def bootstrap_mean(values, n_boot, seed):
    rng = np.random.default_rng(seed)
    idx = rng.integers(0, len(values), size=(n_boot, len(values)))
    return values[idx].mean(axis=1)
```

Rule: every stochastic method should expose `seed` (directly or via `Params`).

## 5) Use explicit, informative names

### Bad

```python
def f(x1, x2):
    return x1 / x2
```

### Good

```python
def incidence_rate(cases, person_years):
    return cases / person_years
```

Readers should understand purpose without opening your notebook narrative.

## 6) Choose data structures intentionally in the analysis pipeline

When students learn statistical coding, many bugs come from using the wrong container.
Use each structure for its strengths.

### 6.1 Dictionary (`dict`): named mappings and settings

Use dictionaries for named configuration, value replacement maps, and style maps.

#### Example A: unified plotting colors and labels

### Bad

```python
# colors repeated manually in multiple places
plt.plot(x, y1, color="blue", label="control")
plt.plot(x, y2, color="red", label="treated")
```

### Good

```python
PLOT_STYLE = {
    "control": {"color": "#1f77b4", "label": "Control"},
    "treated": {"color": "#d62728", "label": "Treated"},
}

plt.plot(x, y1, **PLOT_STYLE["control"])
plt.plot(x, y2, **PLOT_STYLE["treated"])
```

#### Example B: replacement in preprocessing

### Bad

```python
# many chained replacements are hard to read and easy to miss
df["smoker"] = df["smoker"].replace("Yes", 1)
df["smoker"] = df["smoker"].replace("No", 0)
df["sex"] = df["sex"].replace("Female", "F")
df["sex"] = df["sex"].replace("Male", "M")
```

### Good

```python
replace_map = {
    "smoker": {"Yes": 1, "No": 0},
    "sex": {"Female": "F", "Male": "M"},
}

for col, mapping in replace_map.items():
    df[col] = df[col].replace(mapping)
```

### 6.2 List (`list`): ordered steps and collections

Use lists when order matters and items may change.

#### Example: preprocessing step log then export to `recorder.csv`

### Bad

```python
# only print statements, no machine-readable record
print("Dropped missing ages")
print("Winsorized income at 99th percentile")
```

### Good

```python
import pandas as pd

records = []

records.append({
    "step": "drop_missing_age",
    "rows_before": int(n_before),
    "rows_after": int(n_after),
    "note": "Removed rows with missing age",
})

records.append({
    "step": "winsorize_income",
    "p": 0.99,
    "note": "Clipped upper tail",
})

pd.DataFrame(records).to_csv("data/processed/recorder.csv", index=False)
```

This creates a transparent preprocessing audit trail.


### 6.3 Set (`set`): membership checks and uniqueness

Use sets for fast membership checks and deduplication logic.

### Bad

```python
valid_groups = ["control", "treated", "placebo"]
if group in valid_groups:
    ...
```

### Good

```python
valid_groups = {"control", "treated", "placebo"}
if group in valid_groups:
    ...
```

### Quick rule of thumb

- `dict`: "name -> value" mapping (settings, replacement maps, metadata)
- `list`: ordered sequence of items or steps
- `tuple`: fixed-size record that should not be edited
- `set`: unique values and fast membership checks

## 7) Keep notebooks for exploration, scripts for final reruns

### Bad

- only one large notebook with manual cell order dependencies

### Good

- notebook does exploration and explanation
- script runs final pipeline end-to-end

```python
# src/run_analysis.py
from pathlib import Path
from params import Params
from io_utils import load_csv
from cleaning import clean_data


def main():
    p = Params()
    df = load_csv(Path("data/raw/patients.csv"))
    df = clean_data(df)
    df.to_csv("data/processed/patients_clean.csv", index=False)


if __name__ == "__main__":
    main()
```

Minimum standard: `Restart Kernel + Run All` succeeds for shared notebooks.

## 8) Use project-relative paths only

### Bad

```python
df = pd.read_csv("/Users/alex/Desktop/mydata.csv")
```

### Good

```python
from pathlib import Path
import pandas as pd

DATA_RAW = Path("data/raw")
df = pd.read_csv(DATA_RAW / "mydata.csv")
```

This makes your work portable across machines and operating systems.

## 9) Keep raw data immutable

### Bad

- overwriting `data/raw/*.csv` during cleaning

### Good

- read from `data/raw`
- write cleaned outputs to `data/processed`

```python
clean_df.to_csv("data/processed/mydata_clean.csv", index=False)
```

This preserves provenance and makes audits possible.

## 10) Save figures with consistent names and metadata

### Bad

```python
plt.savefig("plot1.png")
```

### Good

```python
from pathlib import Path

FIG_DIR = Path("figs")
FIG_DIR.mkdir(parents=True, exist_ok=True)
plt.savefig(FIG_DIR / "age_histogram_v1.png", dpi=300, bbox_inches="tight")
```

Tip: include units or subgroup in file names when relevant.

## 11) Track package versions

### Bad

- no record of package versions used

### Good

- maintain `requirements.txt` or `environment.yml`
- mention key versions in report appendix
- use `pip freeze` to capture exact versions

Example snippet for report:

```text
Python 3.12
pandas 2.2.2
numpy 2.1.1
statsmodels 0.14.2
scikit-learn 1.5.2
```

## 12) Add lightweight tests for critical calculations

### Bad

- trusting metric code without checks

### Good

```python
# tests/test_rates.py
from src.stats_models import incidence_rate


def test_incidence_rate_simple_case():
    assert incidence_rate(10, 1000) == 0.01
```

Even simple tests catch unit mistakes and denominator bugs.

## 13) Keep a short decision log

### Bad

- dropping outliers without explanation

### Good

Use a short markdown file such as `analysis_decisions.md`:

```text
2026-03-16
- Excluded records with missing outcome.
- Winsorized top 1% of cost variable due to extreme coding errors.
- Chose logistic regression for binary outcome and interpretability.
```

This is very useful when writing methods and limitations sections.

## 14) Commit often with meaningful messages

### Bad

`git commit -m "stuff"`

### Good

`git commit -m "Add missing-value checks to cleaning pipeline"`

Small, meaningful commits help you and your marker understand progress.

## Practical workflow for this course

1. Explore in a notebook.
2. Move reusable code into `src`.
3. Put tunable settings in `src/params.py`.
4. Save cleaned data in `data/processed`.
5. Save figures in `figs`.
6. Run final script from a clean session.
7. Confirm notebook reruns top-to-bottom.

## Quick quality checklist (before submission)

1. Are analysis parameters centralized in one place?
2. Can another student run this on their machine using relative paths?
3. Are random results reproducible via seed?
4. Are data cleaning and statistical calculations separated into functions?
5. Are raw data untouched and processed data written separately?
6. Are figures saved in `figs` with clear names?
7. Is there enough explanation for your modeling choices?

## One-line summary

Write statistical Python code so that another student can rerun, inspect, and trust every result.
