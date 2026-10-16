# AI Adoption at Work: Tool Usage, Productivity & Training Analysis

An exploratory data analysis (EDA) of a survey of **1,205 working professionals and students** on how they use AI tools, how much time they say it saves, and whether they have been trained to use it. Built with Python, Pandas, Matplotlib and Seaborn.

> **Author:** Anuj Kumar | Aspiring Data Analyst / Business Analyst roles
> **LinkedIn:** [linkedin.com/in/anuj-kumar-ssm](https://linkedin.com/in/anuj-kumar-ssm)

---

## 1. Project Overview

Organisations are rolling out AI tools quickly, but it is not always clear which tools people actually use, who has been trained, and whether productivity differs by role. This project cleans a survey dataset and answers a set of focused business questions using descriptive analysis and visualisation.

## 2. Dataset

| Item | Detail |
|---|---|
| Raw size | 1,205 rows x 14 columns |
| Size after cleaning | 1,169 rows x 14 columns |
| Source |  Kaggle DataSet |

**Columns:** `Respondent_ID`, `Age`, `Gender`, `Profession`, `Industry`, `Experience_Level`, `Primary_AI_Tool`, `Primary_Use_Case`, `Daily_AI_Usage_Hours`, `AI_Usage_Frequency`, `AI_Training_Received`, `Estimated_Time_Saved_Minutes_Daily`, `Self_Reported_Productivity_Score`, `Job_Satisfaction_Score_1_to_5`

> Note: productivity, time saved and satisfaction are **self-reported**, so results describe perceptions, not measured output.

## 3. Objectives

1. Find the most popular AI tool.
2. Count respondents by profession.
3. Compare average productivity score by profession.
4. Analyse the gender distribution.
5. Find the minimum, maximum and average age.
6. Estimate the average years of experience.
7. Count how many respondents have received AI training.
8. Compare average daily time saved by AI tool. _(see Challenges: result to be added after re-run)_
9. Show which professions prefer which AI tool (cross-tab heatmap).

## 4. Tools & Technologies

- **Python 3** with **Pandas** (data handling), **Matplotlib** and **Seaborn** (visualisation)
- **Jupyter Notebook**

## 5. Workflow

1. **Load** the CSV and inspect it with `head()`, `tail()`, `info()`, `dtypes`, `columns` and `shape`.
2. **Missing values:** `isnull().sum()` found 31 missing cells in 4 columns (Age 8, Industry 10, Primary_AI_Tool 7, Daily_AI_Usage_Hours 6). Rows with missing values were dropped with `dropna()`.
3. **Duplicates:** `df.duplicated()` flagged 5 exact duplicate rows, removed with `drop_duplicates()`.
4. **Result:** 1,205 -> 1,169 rows (36 rows, about 3%, removed).
5. **Feature engineering:** the text column `Experience_Level` (0-1, 2-5, 6-10, 10+ years) was mapped to numeric midpoints (0.5, 3.5, 8, 11) to estimate an average.
6. **Analysis & charts:** `value_counts()`, `groupby().mean()`, `agg()`, `pd.crosstab()` with count plots, a bar plot, a histogram and a heatmap.

## 6. Key Findings (from the notebook outputs)

| # | Question | Result |
|---|---|---|
| 1 | Most popular AI tool | **ChatGPT: 446 respondents (38.15%)**, then Gemini 251 (21.47%), Microsoft Copilot 237 (20.27%), Claude 137 (11.72%), Other 98 (8.38%) |
| 2 | Respondents by profession | Fairly balanced: Software Developer 157, Marketing 152, Finance 151, Operations 149, Student 148, Data Analyst 143, HR 136, Teacher 133 |
| 3 | Average productivity score by profession | Narrow range, **65.0 to 68.1**: Teacher 68.10, Data Analyst 67.53, HR 66.89, Operations 66.65, Marketing 66.58, Finance 66.28, Student 65.74, Software Developer 65.04 |
| 4 | Gender split | Male 538, Female 531, Prefer not to say 77, Non-binary 23 |
| 5 | Age | Min **18**, max **60**, mean **38.73** |
| 6 | Experience | Estimated mean **4.16 years** (based on assumed category midpoints) |
| 7 | AI training | **735 (about 63%) have not** received AI training; 434 (about 37%) have |

## 7. Business Recommendations

- **Invest in AI training.** Roughly 6 in 10 respondents report no AI training. Training is the clearest gap in the data. _Caveat: this notebook has not yet tested whether trained users report higher productivity, so treat training as a hypothesis to test next._
- **Plan for a multi-tool environment.** ChatGPT leads with about 38%, but more than 60% of respondents use another primary tool. Guidance and governance should cover several tools, not one.
- **Roll out AI support across roles rather than building role-specific programmes first.** Average productivity scores differ by only about 3 points across professions. _Caveat: scores are self-reported and no significance test was run._

## 8. Challenges & Solutions

| Challenge | Root cause | Solution / Status |
|---|---|---|
| Missing values in 4 columns (31 cells) | Incomplete survey responses | Dropped affected rows (about 3% of data). Imputation is listed under future work. |
| 5 duplicate rows | Repeated records at the end of the file | Detected with `duplicated()` and removed with `drop_duplicates()` |
| Q8 (time saved by tool) raised a `NameError` | The plot used `order=tool_time.index`, but the variable is named `tool_time_saved` | Fix: `order=tool_time_saved.index`. **Re-run and add the result here.** |
| Text-based experience levels | Categories, not numbers | Mapped to midpoints. This is an assumption, so 4.16 is an estimate. |
| Some records look inconsistent | e.g. a respondent aged 20 with 6-10 years of experience appears in the displayed rows | Not validated yet. Listed under future improvements. |

## 9. How to Run

```bash
# 1. Clone the repository
git clone https://github.com/<anujkumar026>/ai-adoption-at-work.git
cd ai-adoption-workplace-analysis

# 2. Install dependencies
pip install -r requirements.txt

# 3. Place the dataset in data/ and check the path in the notebook's read_csv line
#    pd.read_csv("../data/ai_adoption.csv")

# 4. Launch the notebook
jupyter notebook notebooks/ai_adoption_analysis.ipynb
```

`requirements.txt`: `pandas`, `matplotlib`, `seaborn`, `jupyter`

Tip: use **Kernel > Restart & Run All** so every output matches the code.

## 10. Future Improvements

- Test whether **AI training** is linked to higher productivity and time saved (`groupby` and a t-test).
- Explore the columns not yet analysed: `Industry`, `Primary_Use_Case`, `Daily_AI_Usage_Hours`, `AI_Usage_Frequency`, `Job_Satisfaction_Score_1_to_5`.
- Check correlations between usage hours, time saved, productivity and satisfaction.
- Replace `dropna()` with imputation (median for numeric, mode for categorical) and compare results.
- Validate data quality (e.g. age vs experience) and check for outliers.
- Build an interactive dashboard (Power BI or Tableau) from the cleaned data.

## 11. Repository Structure

```
ai-adoption-workplace-analysis/
├── data/            #
├── notebooks/      
├── images         
├── README.md
├── requirements.txt
└── .gitignore
```
