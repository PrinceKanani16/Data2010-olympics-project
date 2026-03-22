# DATA 2010 — Olympics Project (1896–2024)

Collaborative DATA 2010 research project using an Olympics dataset (1896–2024).  
This repo focuses on **data cleaning**, **missing values/outlier handling**, **feature engineering**, **exploratory data analysis (EDA)**, and **visualization** in **Jupyter Notebook**.

---

## Course Info
**University of Manitoba — Winter 2026**  
**Course:** DATA 2010 A01 – Tools and Techniques  
**Instructor:** Lie Ding  
**Project Weight:** 15%

**Student:** Prince Kanani  
**Student ID:** 8029853  

**Student:** Josh Mudiwa
**Student ID:** 7954458 


---

## Dataset
**Kaggle:** Olympic Summer and Winter Games (1896–2024)  
https://www.kaggle.com/datasets/magicchris/olympic-summer-and-winter-games-1896-2024

**Owner on Kaggle:** Cassini-Chris (Owner)  
**License:** Apache 2.0  
**Provenance / citation:** Not specified on the Kaggle dataset page.  
**Update frequency:** Not specified on the Kaggle dataset page.

> Note: The raw dataset file is **not included** in this repo. Download it from Kaggle and place it in the `data/` folder.

---

# DATA 2010 Project: Trends in Olympic Athlete Performance and Representation (1896–2024)

## Project overview

This project analyzes the **Olympic Summer and Winter Games (1896–2024)** dataset to study long-run patterns in athlete participation, medal outcomes, country performance, and medal probability.

The project is organized around **three research questions**:

1. **Research Question 1**  
   How do medal outcomes vary by age group and sex, and how did gender parity and typical medal-winning ages change across decades?

2. **Research Question 2**  
   To what extent is country participation size associated with event-medal counts, and how does this relationship shape medal efficiency and Olympic dominance?

3. **Research Question 3**  
   What factors most influence an athlete’s probability of winning a medal, and to what extent does country/team membership contribute to medal probability after accounting for athlete characteristics?

The analysis combines:
- exploratory data analysis,
- feature engineering,
- simple and multiple linear regression,
- logistic regression,
- country-level and athlete-level comparisons,
- figure export for the final report.

## Dataset

**Dataset name:** Olympic Summer and Winter Games (1896–2024)  
**Source:** Kaggle  
**Link:** https://www.kaggle.com/datasets/magicchris/olympic-summer-and-winter-games-1896-2024

### What each row represents
Each row represents **one athlete-event record** for a particular Olympic Games edition. A row includes:
- Olympic year,
- season,
- city,
- sport,
- event,
- team/country,
- athlete sex,
- athlete age,
- medal result.

### Important note about row structure
This dataset does **not** include a unique athlete identifier. Because of that:
- country-level participation is measured using **athlete-event rows**,
- not exact unique athletes,
- team events can inflate medalist rows unless we use an **event-medal** method.

This matters especially for **Research Question 2** and some interpretations in **Research Question 3**.

## Repository / project structure

A recommended structure for this project is:

```text
DATA2010-Olympics-Project/
│
├── README.md
├── notebooks/
│   └── Data2010_Project.ipynb
│
├── data/
│   └── olympics_1896_2024.csv
│
├── figures/
│   ├── RQ1/
│   ├── RQ2/
│   ├── RQ3/
│   └── Appendix/
│
├── outputs/
│   ├── tables/
│   └── model_outputs/
│
└── report/
    └── DATA2010_Project_Report.tex
```

## Required Python packages

Install these packages before running the notebook:

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

## How to run the project

### Step 1: Download the dataset
Download the CSV dataset from Kaggle and place it in your project folder.

Example:
```text
data/olympics_1896_2024.csv
```

### Step 2: Open the notebook
Open the main notebook in Jupyter:

```text
notebooks/Data2010_Project.ipynb
```

### Step 3: Run the notebook in order
Run the notebook **from top to bottom**.

This is important because later sections depend on objects created earlier, such as:
- `df`
- `df_clean`
- `medalists`
- `team_clean`
- `sport_category`
- regression model objects

### Step 4: Make sure output folders exist
Some cells save figures to disk. If your notebook does not already create output folders automatically, create them manually:

```python
import os

os.makedirs("figures", exist_ok=True)
os.makedirs("outputs", exist_ok=True)
```

You may also need subfolders such as:

```python
os.makedirs("figures/RQ1", exist_ok=True)
os.makedirs("figures/RQ2", exist_ok=True)
os.makedirs("figures/RQ3", exist_ok=True)
os.makedirs("figures/Appendix", exist_ok=True)
```

### Step 5: Export plots for the report
The notebook saves selected plots for inclusion in the report. Confirm that the saved image paths match the paths used in the LaTeX report.

## Data cleaning and feature engineering

This project uses several important cleaning and feature-engineering steps.

### 1. Standardizing core columns
We standardize:
- `year`
- `age`
- `medal`
- `sports`
- `team`

### 2. Creating `decade`
We create:

```python
decade = (year // 10) * 10
```

### 3. Creating `age_group`
We convert age into ordered age categories such as:
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

### 4. Creating `won_medal`
We define a binary medal outcome:
- `1` = won Gold, Silver, or Bronze
- `0` = did not win a medal

### 5. Creating `medalists`
For medal-focused descriptive analyses, we create a medalist-only subset.

### 6. Cleaning country/team names
We standardize `team` into a cleaner country/team variable such as `team_clean`.

### 7. Creating sport categories
Detailed sport labels are cleaned into `sports_clean`, then grouped into broader `sport_category` values.

### 8. Creating the event-medal view
For country-level medal counting, we create an **event-medal** dataset by deduplicating medals at:
- `year`
- `event`
- `team_clean`
- `medal`

## Research Question 1

### Main question
How do medal outcomes vary by age group and sex, and how did gender parity and typical medal-winning ages change across decades?

### Main methods used
- 100% stacked bar charts
- decade trend line plots
- median + IQR age plots
- descriptive grouped summaries

## Research Question 2

### Main question
To what extent is country participation size associated with event-medal counts, and how does this relationship shape medal efficiency and Olympic dominance?

### Main methods used
- country-year aggregation
- simple linear regression
- log transformation
- multiple linear regression
- residual plots
- efficiency ranking plots
- dominance comparisons

## Research Question 3

### Main question
What factors most influence an athlete’s probability of winning a medal, and to what extent does country/team membership contribute to medal probability after accounting for athlete characteristics?

### Main methods used
- athlete-level descriptive plot
- logistic regression
- model comparison
- ROC curves
- adjusted country/team effects

## Output files and report figures

Suggested figure organization:

### RQ1
- `plot1.png` — medalist sex composition by age group
- `plot2.png` — medal type composition by age group
- `plot3.png` — gender parity over decades
- `plot4.png` — largest decade-to-decade change in female share
- `plot5.png` — peak medalist age by decade with IQR

### RQ2
- `plot6.png` — participation size vs event medals with least-squares fit
- `plot7.png` — log-transformed relationship
- `plot8.png` — residual plot for multiple regression
- `plot9.png` — top countries by efficiency
- `plot10.png` — dominance plot

### RQ3
- `plot11.png` — medal rate by grouped sport category and sex
- `plot12.png` — ROC curves for logistic regression models
- `plot13.png` — adjusted country/team effects

### Appendix
- `ContinentMedalDistribution.png` — proportion of Olympic medals won by continent

## Reproducibility notes

To keep results reproducible:
- run notebook cells in order,
- keep the same cleaned dataset version,
- ensure train/test split uses a fixed random seed where applicable,
- document any threshold choices or filtering rules.

## Known limitations

1. **No unique athlete identifier**
2. **Team-event inflation**
3. **Combined Summer and Winter Games**
4. **Historical country and sport labels**
5. **Observational analysis**

## Suggested appendix items
- variable definitions table,
- full regression tables,
- supplementary country rankings,
- extra residual or diagnostic plots,
- continent medal distribution,
- feature-engineering summary tables.

## Final checklist before submission
- [ ] dataset path works
- [ ] notebook runs top to bottom without errors
- [ ] all figure paths are correct
- [ ] exported figures match the LaTeX report
- [ ] metrics/tables in report match notebook outputs
- [ ] references and AI disclosure are complete
- [ ] README reflects final notebook and file names


