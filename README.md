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

## Project Overview
The Olympic Games are not only a global competition but also a long-running dataset that can reveal how representation, performance, and strategic investment in sport evolve over time. Using Olympic records spanning **1896–2024**, this project investigates patterns with real-world relevance to athlete development and national sport planning.

---

## Research Questions 
1) **Age × Sex × Sport over decades**  
   How do medal outcomes vary by age group and sex across sports, and which sports show the largest changes in gender parity and peak-age patterns across decades?

2) **Country rankings + efficiency over time**  
   How do country rankings change over time when switching from athlete-medal counts to event-medal counts, and which countries are most efficient (medals per athlete-event entry) under each method across Olympic years?

3) **Sport/event medal production + specialization + stability + host effects**  
   Which sports/events generate the most medal-winning athletes, and how do countries’ medal portfolios (specialization vs diversification) and performance stability change across Olympic editions, especially around host years where medal distribution by sport may shift?

---

## Repository Structure (Suggested)

*Suggested implementation of our repository*

Data2010-olympics-project/
│
├── README.md
├── Research Paper.pdf
├── .gitignore
│
├── data/
│   ├── raw/
│   │   └── olympics_1896_2024.csv
│   └── processed/
│       └── cleaned_olympics.csv
│
├── notebooks/
│   └── Data2010_Project.ipynb
│
├── src/
│   ├── cleaning.py
│   ├── analysis.py
│   └── visualization.py
│
├── figures/
│   ├── RQ1.png
│   ├── RQ1.png
│   ├── RQ1.png
│   ├── RQ1.png
│   ├── figure3.png
│   ├── figur4.png
│   ├── figure5.png
│   └── figure6.png
│
└── report/
    ├── project_template.tex
    └── final_report.pdf
