# DATA 2010 — Olympics Project (1896–2024)

## Trends in Olympic Athlete Performance and Representation

This repository contains our DATA 2010 group project on long-run Olympic participation, medal outcomes, country performance, and athlete-level medal probability using the **Olympic Summer and Winter Games (1896–2024)** dataset.

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

The Olympic Games provide a long historical record of athlete participation and medal outcomes. This project examines how Olympic representation and success changed from **1896 to 2024**.

The analysis is organized around three main research questions:

1. **Research Question 1 — Age, Sex, and Medal Outcomes**  
   How do medal outcomes vary by age group and sex, and how did gender parity and typical medal-winning ages change across decades?

2. **Research Question 2 — Country Participation, Efficiency, and Dominance**  
   To what extent is country participation size associated with event-medal counts, and how does this relationship shape medal efficiency and Olympic dominance?

3. **Research Question 3 — Medal Probability Modeling**  
   What factors most influence an athlete’s probability of winning a medal, and to what extent does country/team membership contribute to medal probability after accounting for athlete characteristics?

### Why This Project Matters

This project is useful for:

- **national sport organizations**, which need evidence for athlete development and talent pipelines;
- **coaches and analysts**, who want fairer ways to compare country performance beyond raw medal totals;
- **journalists and researchers**, who study long-run Olympic trends;
- **policy and funding stakeholders**, who care about how structure, scale, and sport specialization affect success.

### High-Level Findings

Across the report, the overall pattern is that Olympic outcomes are shaped by both **athlete-level** and **country-level** factors:

- female participation rises strongly across decades and moves much closer to parity;
- medal composition varies by age group and sex;
- larger country delegations usually win more medals, but participation size alone does not fully explain medal outcomes;
- logistic regression shows that age, sex, sport, and country/team membership all contribute to medal probability.

---

## Dataset

- **Dataset Name:** Olympic Summer and Winter Games (1896–2024)
- **Source:** Kaggle
- **Link:** https://www.kaggle.com/datasets/magicchris/olympic-summer-and-winter-games-1896-2024
- **Owner on Kaggle:** Cassini-Chris
- **License:** Apache License 2.0

### What One Row Represents

Each row represents **one athlete-event record** for one Olympic Games edition. A row may include:

- year
- season
- sport
- event
- team
- sex
- age
- medal result

### Basic Dataset Facts Used in the Report

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

### Important Structural Note

This dataset does **not** include a unique athlete identifier. That means:

- participation size is measured using **athlete-event rows**, not exact unique athletes;
- team events can inflate athlete-level medal counts;
- country-level medal analysis should use an **event-medal view** to avoid overcounting team medals.

---

## Repository Structure

The repository layout should match the folders shown in GitHub:

```text
.
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

### Folder Purpose

- `Report/` — exported final research paper PDF
- `data/` — raw dataset used in the notebook
- `figures/` — saved plots, organized by research question and appendix
- `notebooks/` — main Jupyter notebook used for the full analysis
- `.gitignore` — Git ignore rules
- `README.md` — project overview and usage instructions

### Figure Folder Purpose

- `figures/RQ1/` — plots used for Research Question 1
- `figures/RQ2/` — plots used for Research Question 2
- `figures/RQ3/` — plots used for Research Question 3
- `figures/Appendix/` — supplementary figures not central to the main three research questions

---

## Tools and Libraries

### Required Python Packages

```bash
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels
```

### Main Libraries Used

- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `scikit-learn`
- `statsmodels`

### Main Analysis Environment

The project is designed to run in **Jupyter Notebook**.

---

## How to Run the Project

### 1. Clone or Download the Repository

Clone this GitHub repository or download it as a ZIP.

### 2. Download the Dataset

Go to the Kaggle dataset page:

```text
https://www.kaggle.com/datasets/magicchris/olympic-summer-and-winter-games-1896-2024
```

Download the CSV file and save it somewhere on your computer.

### 3. Copy the Full Dataset Path

After downloading the CSV file, copy its full file path.

Example paths:

```text
C:/Users/YourName/Downloads/olympics_1896_2024.csv
```

or

```text
C:/Users/YourName/Documents/DATA2010/data/olympics_1896_2024.csv
```

### 4. Open the Notebook

Open:

```text
notebooks/Data2010_Project.ipynb
```

### 5. Paste Your Dataset Path into the Notebook

In the data-loading section of the notebook, replace the existing dataset path with the full path to your downloaded CSV file.

Example:

```python
file_path = r"C:/Users/YourName/Downloads/olympics_1896_2024.csv"
df = pd.read_csv(file_path)
```

If you moved the file into the repository `data/` folder, you can instead use:

```python
file_path = r"data/olympics_1896_2024.csv"
df = pd.read_csv(file_path)
```

### 6. Run All Notebook Cells in Order

Run the notebook from top to bottom. This is important because later sections depend on cleaned datasets and engineered variables created earlier.

Examples of objects reused later include:

- `df`
- `df_clean`
- `medalists`
- `team_clean`
- `sport_category`
- regression model objects
- train/test split objects for logistic regression

### 7. Make Sure Output Folders Exist

If needed, run:

```python
import os

os.makedirs("figures", exist_ok=True)
os.makedirs("figures/RQ1", exist_ok=True)
os.makedirs("figures/RQ2", exist_ok=True)
os.makedirs("figures/RQ3", exist_ok=True)
os.makedirs("figures/Appendix", exist_ok=True)
```

### 8. Check Saved Plot Paths

Before exporting plots or committing changes, confirm that:

- plot files are saved into the correct `figures/RQ1`, `figures/RQ2`, `figures/RQ3`, or `figures/Appendix` folder;
- filenames are clear and match the report;
- notebook output paths match repository folder names.

---

## Data Cleaning and Feature Engineering

The project includes substantial cleaning and feature engineering before analysis.

### Main Cleaning Steps

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

### Example Engineered Variables

- `age_group`
- `won_medal`
- `medal_points`
- `team_clean`
- `sports_clean`
- `sport_category`

---

## Research Questions and Methods

## Research Question 1

**Question:** How do medal outcomes vary by age group and sex, and how did gender parity and typical medal-winning ages change across decades?

### Methods Used

- descriptive summaries
- grouped comparisons
- 100% stacked bar charts
- decade-level share plots
- median + IQR trend plots

### Main Figures

- Medalist share by age group (100% stacked by sex)
- Gender parity over time by decade
- Largest decade-to-decade changes in female share
- Overall peak medalist age by decade with IQR

### Main Conclusion

Olympic participation becomes much more gender-balanced over time, while medalist composition and typical medal-winning ages vary across age groups and by sex.

---

## Research Question 2

**Question:** To what extent is country participation size associated with event-medal counts, and how does this relationship shape medal efficiency and Olympic dominance?

### Methods Used

- country-year aggregation
- scatterplots
- least-squares regression
- log transformation
- multiple linear regression
- residual analysis
- efficiency ranking
- dominance comparisons

### Main Figures

- Participation size vs. event medals with least-squares fit
- Log-transformed participation size vs. event medals
- Residual plot for the multiple regression model
- Top countries by medal efficiency
- Dominance in a selected Olympic year

### Main Conclusion

Larger delegations generally win more event medals, but participation size alone does not fully explain country success. Log transformation and multiple regression improve the analysis, while efficiency plots show that countries with similar participation levels can perform very differently.

---

## Research Question 3

**Question:** What factors most influence an athlete’s probability of winning a medal, and to what extent does country/team membership contribute to medal probability after accounting for athlete characteristics?

### Methods Used

- grouped descriptive comparisons
- athlete-level binary target construction
- logistic regression
- model comparison
- ROC curves
- adjusted country/team effect visualization

### Main Figures

- Medal rate by grouped sport category and sex, with dominant medal-winning age-bin labels
- ROC curves comparing the athlete-level logistic regression model
- Country/team effects from the logistic regression model after controlling for key athlete characteristics

### Main Conclusion

Age, sex, and sport category all matter for medal probability, but adding country/team membership improves classification performance further. This suggests that country-level advantages remain important even after athlete-level variables are included.

---

## Expected Figure Outputs

### `figures/RQ1/`
- RQ1 plots used in the report

### `figures/RQ2/`
- RQ2 plots used in the report

### `figures/RQ3/`
- RQ3 plots used in the report

### `figures/Appendix/`
- supplementary figures such as extra diagnostics, supporting visuals, or non-core plots

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

- **Prince Kanani:** selection and refinement of the research questions; most of the data cleaning and feature engineering; development of the sport-category grouping; organization of the main notebook analysis; visualization coding; figure selection for the final report; regression and logistic-regression modeling and model comparison; notebook interpretations, conclusions, and limitations; and reproducibility through GitHub organization and template integration.

- **Joshua Mudiwa:** project overview and scope definition; support with data cleaning and country/team grouping; figure organization and appendix exploration; contributions to the data source and description section; support on the data-analysis write-up; report formatting, structure, and presentation; and contributions to conclusions, limitations, next steps, and overall report quality.
