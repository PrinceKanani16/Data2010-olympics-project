# DATA 2010 — Olympics Project (1896–2024)

**Trends in Olympic Athlete Performance and Representation**

Collaborative DATA 2010 project analyzing long-run Olympic participation, medal outcomes, country performance, and athlete-level medal probability using the **Olympic Summer and Winter Games (1896–2024)** dataset.

---

## Course Information

- **University:** University of Manitoba
- **Course:** DATA 2010 A01 — Tools and Techniques
- **Term:** Winter 2026
- **Instructor:** Lei Ding
- **Project Type:** Group project

### Authors
- **Prince Kanani** — 8029853
- **Joshua Mudiwa** — 7954458

---

## Project Overview

The Olympic Games provide a long historical record of athlete participation and medal outcomes. This project uses that record to study how Olympic representation and success changed from **1896 to 2024**.

The analysis is organized around **three main research questions**:

1. **Research Question 1 — Age, sex, and medal outcomes**  
   How do medal outcomes vary by age group and sex, and how did gender parity and typical medal-winning ages change across decades?

2. **Research Question 2 — Country participation, efficiency, and dominance**  
   To what extent is country participation size associated with event-medal counts, and how does this relationship shape medal efficiency and Olympic dominance?

3. **Research Question 3 — Medal probability modeling**  
   What factors most influence an athlete’s probability of winning a medal, and to what extent does country/team membership contribute to medal probability after accounting for athlete characteristics?

### Why this project matters

This project is useful for:

- **national sport organizations**, which need evidence for athlete development and talent pipelines;
- **coaches and analysts**, who want fairer ways to compare country performance beyond raw medal totals;
- **journalists and researchers**, who study long-run Olympic trends;
- **policy and funding stakeholders**, who care about how structure, scale, and specialization affect success.

### High-level findings

Across the report, the main pattern is that Olympic outcomes are shaped by both **athlete-level** and **country-level** factors:

- female participation rises strongly across decades and moves much closer to parity;
- medal composition varies by age group and sex;
- larger country delegations usually win more medals, but participation size alone does not fully explain medal outcomes;
- logistic regression shows that age, sex, sport, and country/team membership all contribute to medal probability.

---

## Dataset

- **Dataset name:** Olympic Summer and Winter Games (1896–2024)
- **Source:** Kaggle
- **Link:** https://www.kaggle.com/datasets/magicchris/olympic-summer-and-winter-games-1896-2024
- **Owner on Kaggle:** Cassini-Chris
- **License:** Apache License 2.0
- **Authors / provenance / DOI:** Not specified on the Kaggle page

### What one row represents

Each row represents **one athlete-event record** for one Olympic Games edition. A row may include:

- year
- season
- sport
- event
- team
- sex
- age
- medal result

### Basic dataset facts used in the report

| Item | Value |
|---|---:|
| Rows | 290,697 |
| Columns | 8 |
| Year range | 1896–2024 |
| Seasons | Summer and Winter |
| Unique years | 38 |
| Unique teams | 1,151 |
| Unique sports | 92 |
| Unique events | 1,534 |
| Medalist rows (Gold/Silver/Bronze) | 42,756 |
| Non-medalist rows | 247,941 |
| Age range | 10–72 |
| Sex proportion | 69.38% M / 30.62% F |
| Exact duplicate rows removed | 0 |

### Important structural note

This dataset does **not** include a unique athlete identifier. That has important consequences:

- participation size is measured using **athlete-event rows**, not exact unique athletes;
- team events can inflate athlete-level medal counts;
- country-level medal analysis should use an **event-medal view** to avoid overcounting team medals.

This limitation matters especially for country-level comparisons and predictive modeling.

---

## Repository Structure

```text
├── Report/
│   └── Research_Paper.pdf
├── data/
│   └── olympics_1896_2024.csv
├── figures/
│   ├── Appendix/
│   ├── RQ1/
│   ├── RQ2/
│   └── RQ3/
├── notebooks/
│   └── Data2010_Project.ipynb
├── .gitignore
└── README.md
```

### Folder purpose

- `notebooks/` — main Jupyter notebook for loading, cleaning, analyzing, and plotting
- `data/` — raw dataset file used by the notebook
- `RQ1_plots/`, `RQ2_plots/`, `RQ3_plots/` — exported plots used in the report
- `outputs/` — saved tables, summaries, and model outputs
- `report/` — final report and report assets
- `Appendix/` — supplementary figures and tables

---

## Tools and Libraries

### Required Python packages

```bash
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels
```

### Main libraries used

- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `scikit-learn`
- `statsmodels`

### Main analysis environment

The project is designed to run in **Jupyter Notebook**.

---

## How to Run the Project

### 1. Clone or download the repository

Download this repository to your machine.

### 2. Download the dataset

Download the Kaggle CSV file and place it inside the `data/` folder.

Expected path:

```text
data/olympics_1896_2024.csv
```

### 3. Open the notebook

Open the main notebook:

```text
notebooks/Data2010_Project.ipynb
```

### 4. Run all cells in order

Run the notebook from top to bottom. This is important because later sections depend on cleaned datasets and engineered variables created earlier.

Examples of objects reused later include:

- `df`
- `df_clean`
- `medalists`
- `team_clean`
- `sport_category`
- regression model objects
- train/test split objects for logistic regression

### 5. Create output folders if needed

If the notebook does not already create folders automatically, run:

```python
import os

os.makedirs("outputs", exist_ok=True)
os.makedirs("RQ1_plots", exist_ok=True)
os.makedirs("RQ2_plots", exist_ok=True)
os.makedirs("RQ3_plots", exist_ok=True)
os.makedirs("Appendix", exist_ok=True)
```

### 6. Check saved output paths

Before exporting plots or tables, confirm that:

- figure paths in the notebook match the report paths;
- filenames are consistent across notebook, outputs, and report;
- saved tables are written into the expected folders.

---

## Data Cleaning and Feature Engineering

The project includes substantial cleaning and feature engineering before analysis.

### Main cleaning steps

1. **Standardized core columns**  
   Standardized columns such as `team`, `sports`, `event`, and `medal`, and stripped extra whitespace from text fields.

2. **Created binary medal outcome**  
   Built `won_medal` to indicate whether a row resulted in Gold, Silver, or Bronze.

3. **Created ordered age groups**  
   Built age bins for clearer comparisons in tables and plots.

4. **Created medal points**  
   Used medal points for descriptive summaries of success.

5. **Cleaned country/team labels**  
   Created `team_clean` so country-level summaries would be consistent and interpretable.

6. **Grouped sports into broader categories**  
   Reduced detailed sport labels into cleaner `sport_category` groupings for Research Question 3.

7. **Built an event-medal view**  
   Deduplicated medals at `(year, event, team_clean, medal)` so team events would not inflate country medal totals.

8. **Built country-year summaries**  
   Created aggregated country-year variables such as participation size, event-medal counts, efficiency, number of sports, and year.

### Example engineered variables

- `age_group`
- `won_medal`
- `medal_points`
- `team_clean`
- `sports_clean`
- `sport_category`
- country-year summary variables

### Example age-group structure

The project uses ordered age bins such as:

- `<16`
- `16–18`
- `19–21`
- `22–24`
- `25–27`
- `28–30`
- `31–35`
- `36–40`
- `41–50`
- `51+`

### Before-and-after cleaning summary

| Check | Before cleaning | After cleaning |
|---|---|---|
| Country/team labels | historical names, spelling variation, and non-country teams | cleaned to `team_clean` |
| Sport labels | overly detailed / inconsistent | standardized and grouped |

---

## Research Questions and Methods

## Research Question 1

**Question:** How do medal outcomes vary by age group and sex, and how did gender parity and typical medal-winning ages change across decades?

### Methods used

- descriptive summaries
- grouped comparisons
- 100% stacked bar charts
- decade-level share plots
- median + IQR trend plots

### Main figures

- Medalist share by age group (100% stacked by sex)
- Gender parity over time by decade
- Largest decade-to-decade changes in female share
- Overall peak medalist age by decade with IQR

### Main conclusion

The project finds that Olympic participation becomes much more gender-balanced over time, while medalist composition and typical medal-winning ages vary across age groups and by sex.

---

## Research Question 2

**Question:** To what extent is country participation size associated with event-medal counts, and how does this relationship shape medal efficiency and Olympic dominance?

### Methods used

- country-year aggregation
- scatterplots
- least-squares regression
- log transformation
- multiple linear regression
- residual analysis
- efficiency ranking
- dominance comparisons

### Main figures

- Participation size vs. event medals with least-squares fit
- Log-transformed participation size vs. event medals
- Residual plot for the multiple regression model
- Top countries by medal efficiency
- Dominance in a selected Olympic year

### Main conclusion

Larger delegations generally win more event medals, but participation size alone does not fully explain country success. Log transformation and multiple regression improve the analysis, while efficiency plots show that countries with similar participation levels can perform very differently.

---

## Research Question 3

**Question:** What factors most influence an athlete’s probability of winning a medal, and to what extent does country/team membership contribute to medal probability after accounting for athlete characteristics?

### Methods used

- grouped descriptive comparisons
- athlete-level binary target construction
- logistic regression
- model comparison
- ROC curves
- adjusted country/team effect visualization

### Main figures

- Medal rate by grouped sport category and sex
- ROC curves for logistic regression models
- Adjusted country/team effects from logistic regression

### Main conclusion

Age, sex, and sport category all matter for medal probability, but adding country/team membership improves classification performance further. This suggests that country-level advantages remain important even after athlete-level variables are included.

---

## Modeling Summary

### Regression for RQ2

The report uses:

- a **simple regression** as a baseline using participation size alone;
- a **log-transformed analysis** to improve visibility and linearity;
- a **multiple regression** using predictors such as log participation size, number of sports, and year.

### Classification for RQ3

The report uses logistic regression because medal success is a **binary outcome**.

Two models are compared:

- **Model A:** age + sex + sport category
- **Model B:** age + sex + sport category + country/team membership

The extended model performs better than the athlete-only baseline, indicating that country/team contributes additional predictive information.

---

## Expected Outputs

### Figures

#### `RQ1_plots/`
- `plot1.png` — medalist sex composition by age group
- `plot3.png` — gender parity over decades
- `plot4.png` — largest decade-to-decade change in female share
- `plot5.png` — peak medalist age by decade with IQR

#### `RQ2_plots/`
- `plot6.png` — participation size vs. event medals with least-squares fit
- `plot7.png` — log-transformed relationship
- `plot8.png` — residual plot for multiple regression
- `plot9.png` — top countries by medal efficiency
- `plot10.png` — dominance plot

#### `RQ3_plots/`
- `plot11.png` — medal rate by grouped sport category and sex
- `plot12.png` — ROC curves for logistic regression models
- `plot13.png` — adjusted country/team effects

#### `Appendix/`
- `ContinentMedalDistribution.png` — supplementary medal distribution figure
- supplementary tables and extra visuals

### Outputs

Suggested saved outputs include:

- cleaned summary tables
- regression diagnostics
- model metrics
- appendix tables
- country rankings
- exported coefficient or odds-ratio summaries

---

## Reproducibility Notes

To keep the project reproducible:

- run notebook cells in order;
- keep dataset path names consistent;
- use the same cleaned-data pipeline each time;
- fix random seeds for train/test split or any random process;
- document thresholds and filtering rules clearly;
- make sure exported filenames match the report.

---

## Known Limitations

1. **No unique athlete identifier**  
   Participation is measured with athlete-event rows rather than exact unique athletes.

2. **Team-event inflation**  
   Athlete-level medal counts can overstate country success unless event-medal deduplication is used.

3. **Combined Summer and Winter Games**  
   Combining both may hide meaningful differences across Olympic types.

4. **Historical label inconsistency**  
   Country/team and sport names vary historically and require careful cleaning.

5. **Observational, not causal**  
   Regression and logistic regression show associations, not causal effects.

6. **Incomplete comparability across years**  
   The report notes that the dataset is missing the **2018 Winter Olympics**, which affects some time-based dominance comparisons.

---

## Real-World Relevance

Based on the report, the results support three practical recommendations:

- **Use age- and sex-specific development pathways** rather than assuming the same peak-performance structure across all athletes.
- **Do not rely only on raw medal totals** when comparing countries; medal efficiency and participation context also matter.
- **Combine athlete-level and country-level planning** because structural national advantages still appear in medal probability models.

---

## Contributions

- **Prince Kanani** — data cleaning, feature engineering, RQ1 structure, regression and logistic-regression setup, interpretation writing, and final report integration
- **Joshua Mudiwa** — plot integration, report formatting, figure organization, review of written sections, and support on report structure and presentation

---

## References and Related Materials

Main project references include:

- Olympic Summer and Winter Games (1896–2024), Kaggle dataset
- DATA 2010 course notes on pandas, regression, and logistic regression
- pandas documentation
- scikit-learn documentation
- statsmodels documentation

---

## Final Checklist Before Submission

- [ ] dataset path works
- [ ] notebook runs top to bottom without errors
- [ ] figure paths are correct
- [ ] exported figures match the report
- [ ] metrics and tables in the report match notebook outputs
- [ ] README reflects final notebook and folder names
- [ ] references and AI disclosure are complete
