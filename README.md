# ECE 2112: Advanced Computer Programming and Algorithms

## Experiment 4: Data Wrangling and Data Visualization

**Student Name:** Bendicio, Sedric Lance B.  
**Section:** 2ECE-A  
**Date Submitted:** September 18, 2026

---

## Table of Contents

1. [Objectives](#i-objectives)
2. [Repository Contents](#ii-repository-contents)
3. [Dataset Overview](#iii-dataset-overview)
4. [Detailed Problem Solutions and Discussion](#iv-detailed-problem-solutions-and-discussion)
   - [Problem A: Visayas Communication DataFrame](#problem-a-visayas-communication-dataframe)
   - [Problem B: Visayas Female DataFrame](#problem-b-visayas-female-dataframe)
   - [Problem C: Category-Average Visualization](#problem-c-category-average-visualization)
5. [Methods Used](#v-methods-used)
6. [Constraints and Compliance Checklist](#vi-constraints-and-compliance-checklist)
7. [How to Run](#vii-how-to-run)

---

## I. Objectives

At the end of this laboratory activity, the student should be able to:

1. Filter tabular data using several categorical and numerical conditions.
2. Construct focused DataFrames by selecting relevant features.
3. Summarize the relationship between categorical features and a numerical variable.
4. Communicate a data comparison using clear and correctly labeled plots.

The problems require the use of the ECE Board Exam 2 dataset and Pandas-based data manipulation. The original DataFrame is kept unchanged except for the derived `Average` column used by the notebook.

---

## II. Repository Contents

| File | Description |
|---|---|
| `Programming Assignment 4 (BENDICIO_2ECE-A).ipynb` | Executed Jupyter Notebook containing the Python code, generated DataFrames, summary tables, and visualization. |
| `board2.csv` | Input dataset containing the ECE Board Exam 2 student records. |
| `README.md` | Documentation of the objectives, methods, solutions, code snippets, test outputs, and execution instructions. |

---

## III. Dataset Overview

The activity uses the **ECE Board Exam 2** dataset. The notebook loads the data using Pandas:

```python
import pandas as pd
import matplotlib.pyplot as plt

ECE_BE_2 = pd.read_csv('board2.csv')
```

The dataset used by the notebook contains **30 student records** and the following fields:

- `Name`
- `Gender`
- `Track`
- `Hometown`
- `Math`
- `Electronics`
- `GEAS`
- `Communication`

The notebook derives the `Average` value from the four subject scores:

```python
ECE_BE_2['Average'] = (
    ECE_BE_2.Math
    + ECE_BE_2.Electronics
    + ECE_BE_2.GEAS
    + ECE_BE_2.Communication
) / 4
```

### Average Formula

Average = (Math + Electronics+ GEAS + Communication) / 4

This derived column is then used in Problems A, B, and C.

---

# IV. Detailed Problem Solutions and Discussion

## Problem A: Visayas Communication DataFrame

### Problem Statement

Create a DataFrame named `VisComm` containing students who:

1. Have `Hometown` equal to `Visayas`; and
2. Have `Track` equal to `Communication`.

Only the following columns must be retained, in this order:

`Name`, `Gender`, `Math`, `Electronics`, `Average`

The resulting DataFrame and its number of rows must be displayed.

### Method Used

The solution uses **Boolean indexing** with two conditions joined by the `&` operator. The selected columns are then specified using a column list.

```python
VisComm = ECE_BE_2[
            (ECE_BE_2['Hometown'] == 'Visayas') & 
             (ECE_BE_2['Track'] == 'Communication')
             ][['Name', 'Gender', 'Math', 'Electronics', 'Average']]

display (VisComm)

print ("Number of rows:", len (VisComm))
```

### How the Code Works

- `ECE_BE_2['Hometown'] == 'Visayas'` identifies students from Visayas.
- `ECE_BE_2['Track'] == 'Communication'` identifies students under the Communication track.
- `&` requires **both conditions** to be true.
- The final column list keeps only the required five features.
- `len(VisComm)` counts the resulting records.

### Test Case / Expected Output

| Index | Name | Gender | Math | Electronics | Average |
|---:|---|---|---:|---:|---:|
| 10 | S11 | Female | 48 | 56 | 54.75 |
| 11 | S12 | Male | 89 | 67 | 76.00 |
| 17 | S18 | Male | 81 | 40 | 63.50 |
| 21 | S22 | Female | 64 | 39 | 62.50 |
| 27 | S28 | Male | 85 | 53 | 67.75 |

**Number of rows: `5`**

### Result

The filtering operation successfully returns **5 students** who satisfy both the Visayas hometown condition and the Communication track condition.

---

## Problem B: Visayas Female DataFrame

### Problem Statement

Create a DataFrame named `VisFemale` containing students who:

1. Have `Hometown` equal to `Visayas`; and
2. Have `Gender` equal to `Female`.

Only these columns should be retained:

`Name`, `Track`, `GEAS`, `Electronics`, `Average`

After creating `VisFemale`, display only the records whose `Average` is at least `60`. The original `VisFemale` DataFrame must not be overwritten.

### Method Used

The solution again uses **Boolean indexing**, but the second filtering operation is applied to the already-created `VisFemale` DataFrame.

```python
ECE_BE_2 ['Average'] = ((ECE_BE_2.Math + ECE_BE_2.Electronics + ECE_BE_2.GEAS + ECE_BE_2.Communication)/4)
VisFemale = ECE_BE_2[
            (ECE_BE_2['Hometown'] == 'Visayas') & 
             (ECE_BE_2['Gender'] == 'Female')
             ][['Name', 'Track', 'GEAS', 'Electronics', 'Average']]


print ("\n\033[1m" + "\t    Female Takers from Visayas" + "\033[0m")
display (VisFemale)
print ("Number of rows:", len (VisFemale))

print ("\n\033[1m" + "Female Takers from Visayas with Greater than 60 Average" + "\033[0m")
display (VisFemale[VisFemale['Average'] >= 60])
print ("Number of rows:", len (VisFemale[VisFemale['Average'] >= 60]))
```

### How the Code Works

- The first Boolean expression selects students from Visayas.
- The second Boolean expression selects female students.
- `&` combines the two conditions so both must be satisfied.
- The column list keeps only the required features.
- `VisFemale[VisFemale['Average'] >= 60]` creates a separate filtered result.
- `VisFemale` remains unchanged.

### Test Case 1: Complete `VisFemale`

| Index | Name | Track | GEAS | Electronics | Average |
|---:|---|---|---:|---:|---:|
| 5 | S6 | Microelectronics | 86 | 45 | 75.50 |
| 10 | S11 | Communication | 48 | 56 | 54.75 |
| 20 | S21 | Microelectronics | 68 | 51 | 68.50 |
| 21 | S22 | Communication | 89 | 39 | 62.50 |
| 23 | S24 | Microelectronics | 60 | 45 | 57.75 |
| 25 | S26 | Instrumentation | 83 | 47 | 65.75 |

**Number of rows: `6`**

### Test Case 2: `Average >= 60`

| Index | Name | Track | GEAS | Electronics | Average |
|---:|---|---|---:|---:|---:|
| 5 | S6 | Microelectronics | 86 | 45 | 75.50 |
| 20 | S21 | Microelectronics | 68 | 51 | 68.50 |
| 21 | S22 | Communication | 89 | 39 | 62.50 |
| 25 | S26 | Instrumentation | 83 | 47 | 65.75 |

**Number of rows: `4`**

### Result

The first filter produces **6 female students from Visayas**. Applying the numerical condition `Average >= 60` produces **4 qualifying records**, while the original `VisFemale` DataFrame remains intact.

---

## Problem C: Category-Average Visualization

### Problem Statement

Examine how the recorded `Average` differs across:

1. `Track`
2. `Gender`
3. `Hometown`

The task requires:

- Computing the mean `Average` for every category.
- Displaying the three summary tables.
- Creating one figure containing three bar charts.
- Identifying the category with the highest **sample mean** for each feature.
- Interpreting only the observed dataset; group means do not by themselves establish causation.

### Method Used

The solution uses Pandas `groupby()` and `mean()` to calculate the category-level averages.

```python
mean_track = pd.DataFrame(ECE_BE_2.groupby(['Track'])['Average'].mean().reset_index())

mean_gender = pd.DataFrame(ECE_BE_2.groupby(['Gender'])['Average'].mean().reset_index())

mean_hometown = pd.DataFrame(ECE_BE_2.groupby(['Hometown'])['Average'].mean().reset_index())
```

### Test Case 1: Mean Average by Track

| Track | Average |
|---|---:|
| Communication | 67.975 |
| Instrumentation | 65.225 |
| Microelectronics | 67.500 |

The highest observed sample mean in the Track summary is **Communication: 67.975**.

### Test Case 2: Mean Average by Gender

| Gender | Average |
|---|---:|
| Female | 66.616667 |
| Male | 67.183333 |

The highest observed sample mean in the Gender summary is **Male: 67.183333**.

### Test Case 3: Mean Average by Hometown

| Hometown | Average |
|---|---:|
| Luzon | 68.083333 |
| Mindanao | 66.678571 |
| Visayas | 65.750000 |

The highest observed sample mean in the Hometown summary is **Luzon: 68.083333**.

### Visualization Code

A figure with three separate bar charts can be produced as follows:

```python
plt.figure(figsize=(20, 8))
plt.ylim(0, 100)
plt.title("Mean Average by Track                                                          Mean Average by Gender                                                    Mean Average by Hometown")
mean_track_graph = plt.bar(mean_track['Track'], mean_track['Average'])
plt.bar_label(mean_track_graph, label_type='edge')

mean_gender_graph = plt.bar(mean_gender['Gender'], mean_gender['Average'])
plt.bar_label(mean_gender_graph, label_type='edge')

mean_hometown_graph = plt.bar(mean_hometown['Hometown'], mean_hometown['Average'])
plt.bar_label(mean_hometown_graph, label_type='edge')
```

<img width="1603" height="678" alt="image" src="https://github.com/user-attachments/assets/db3c3d64-50b5-45e1-bccd-275ae6d98254" />

### Interpretation

Based strictly on the sample used in the dataset:

- **Track:** Communication has the highest sample mean `Average` at **67.975**.
- **Gender:** Male students have the highest sample mean `Average` at **67.183333**.
- **Hometown:** Students from Luzon have the highest sample mean `Average` at **68.083333**.

These statements describe the observed dataset only. They do **not** establish that Track, Gender, or Hometown causes a higher board-exam score.

---

# V. Methods Used

| Method / Function | Purpose |
|---|---|
| `pd.read_csv()` | Loads `board2.csv` into a Pandas DataFrame. |
| `DataFrame['column']` | Accesses a specific column. |
| `==` | Tests whether a column value matches a required category. |
| `&` | Combines multiple Boolean conditions where all conditions must be true. |
| `DataFrame[condition]` | Filters rows according to a Boolean condition. |
| `DataFrame[[columns]]` | Selects only the required columns. |
| `len()` | Determines the number of rows in a DataFrame. |
| `groupby()` | Groups records according to a categorical feature. |
| `mean()` | Calculates the arithmetic mean of `Average` for each group. |
| `reset_index()` | Converts grouped results back into a regular DataFrame structure. |
| `plt.bar()` | Creates bar charts for category comparisons. |
| `set_ylim()` | Keeps the visualization on a consistent 0–100 scale. |
| `bar_label()` | Displays the numerical value on each bar. |

---

# VI. Constraints and Compliance Checklist

- [x] **Dataset-derived results:** All DataFrame rows, category means, and plotted values are derived from `board2.csv`.
- [x] **No manual category means:** The category means are calculated using Pandas `groupby()` and `mean()`.
- [x] **Visualization scale:** The bar charts use a consistent `0–100` scale appropriate for the average scores for board exams.

---

# VII. How to Run

### 1. Clone the Repository

```bash
git clone <YOUR-GITHUB-REPOSITORY-URL>
cd <YOUR-REPOSITORY-FOLDER>
```

### 2. Install the Required Libraries

```bash
pip install pandas matplotlib jupyter
```

### 3. Make Sure the Dataset Is Available

Place `board2.csv` in the same directory as the Jupyter Notebook:

```text
repository/
├── board2.csv
├── Programming Assignment 4 (BENDICIO_2ECE-A).ipynb
└── README.md
```

### 4. Launch Jupyter Notebook

```bash
jupyter notebook "Programming Assignment 4 (BENDICIO_2ECE-A).ipynb"
```

### 5. Execute the Notebook

Run all cells from top to bottom. The notebook should generate:

1. The derived `Average` column.
2. `VisComm` and its row count.
3. `VisFemale` and the `Average >= 60` filtered result.
4. Mean `Average` summaries by Track, Gender, and Hometown.
5. The category-average visualization.
6. The three interpretation statements.

---

## Summary of Results

| Problem | Result |
|---|---|
| **A. VisComm** | 5 students from Visayas under the Communication track |
| **B. VisFemale** | 6 female students from Visayas; 4 have `Average >= 60` |
| **C. Track Mean** | Communication — 67.975 |
| **C. Gender Mean** | Male — 67.183333 |
| **C. Hometown Mean** | Luzon — 68.083333 |
