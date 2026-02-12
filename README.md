![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# Lab | pandas Foundations for Labeled Data

## Overview

This lab focuses on working with labeled data in pandas. You will build a small dataset about class attendance, load it into a DataFrame, and use Series and DataFrame operations to clean, filter, and summarize it. The emphasis is on understanding labels, indexes, and alignment so that your analysis is correct and reproducible.

## Learning Goals

By the end of the lab, you should be able to create and inspect pandas Series and DataFrames, set and use indexes intentionally, perform label-based selection, and validate results with simple checks. You should also be able to explain how alignment affects arithmetic and assignments.

## Setup and Context

You will generate a synthetic dataset in code representing weekly class attendance for a training program. Each row includes a student ID, cohort, attended sessions, and expected sessions. You will build the dataset in Python, then load it into pandas. The dataset is intentionally small so you can reason about it directly while still practicing real workflows. Work in a notebook named `m1-05-pandas-foundations-lab.ipynb`.

## Requirements

- Fork this repository to your own GitHub account.
- Clone your fork to your machine.
- Make sure you can open and run Jupyter notebooks (for example via Jupyter Lab or VS Code).

## Getting Started

- Create a new notebook and name it `m1-05-pandas-foundations-lab.ipynb`.
- Before you submit, restart your kernel and run the notebook **top to bottom**.
- As you work, prefer pandas vectorized operations over Python loops.

## Tasks

### Task 1: Build and load the dataset

Create a list of dictionaries called `attendance_raw` with exactly 24 records. Each record must include:
1. `student_id` in the format `S001` to `S024`
2. `cohort` as one of `["alpha", "beta", "gamma"]`
3. `attended_sessions` as an integer between 0 and 6
4. `expected_sessions` as the integer 6

Then load the list into a DataFrame named `attendance`. Print the first five rows and call `info()` to confirm the structure and data types.

### Task 2: Set an index and validate alignment

Set `student_id` as the index and store the result in `attendance_indexed`. Create a Series named `excused_absences` with at least 10 student IDs (some IDs must not exist in the DataFrame). Add this Series to `attended_sessions` to create a new column `adjusted_attendance`. Confirm that rows without matching IDs become missing in `adjusted_attendance`. Then fill missing values in `adjusted_attendance` with the original `attended_sessions` and show the updated column.

### Task 3: Clean and normalize categories

Introduce a small inconsistency by modifying a few `cohort` values to include extra whitespace and inconsistent casing. Then write pandas code to normalize the `cohort` column by stripping whitespace and converting to lowercase. After cleaning, display the unique cohorts to confirm that the inconsistencies are resolved.

### Task 4: Filter and compute summaries

Filter the DataFrame to students where `attended_sessions` is below `expected_sessions`. Store the result in `low_attendance`. Compute the average `attended_sessions` by cohort using `groupby`. Print the summary and verify that cohorts in the summary match the cleaned cohorts.

### Task 5: Add a derived field and validate it

Create a new column `attendance_ok` that is `True` when `attended_sessions` is at least 5, otherwise `False`. Use a boolean comparison rather than a loop. Then validate the column by confirming that every row in `low_attendance` has `attendance_ok` equal to `False`.

## Common Pitfalls and Debugging Notes

A common mistake is confusing label-based and position-based indexing. If you use `iloc` when you intended `loc`, you may select the wrong rows. Another common issue is forgetting that Series alignment happens by index, not by order. If your `adjusted_attendance` column has missing values, check whether the index values actually match.

Be careful when cleaning text columns. Use vectorized string methods and confirm the results by checking `unique()` values. Small casing or whitespace issues can lead to misleading groupby results.

## Submission

### What to submit

Submit the following files:
- The notebook file `m1-05-pandas-foundations-lab.ipynb`

### Definition of done (checklist)

Before you submit, make sure:

- [ ] The notebook runs **top to bottom** without errors after a kernel restart.
- [ ] Your dataset has exactly 24 records and uses `S001` to `S024` as specified.
- [ ] You demonstrated index alignment behavior (including missing IDs in the Series and the resulting missing values).
- [ ] Cohort cleaning is validated with `unique()` (or equivalent).
- [ ] Your derived `attendance_ok` column is validated against `low_attendance`.
- [ ] The notebook is saved and included in your git commit.

### How to submit (Git workflow)

- When you’re done, make sure all changes are saved, then run:

```bash
git add .
git commit -m "Solved m1-05 lab"
git push -u origin HEAD
```

- Make a pull request.
- Paste the link to your pull request in the Student Portal.

## Evaluation Criteria

Your work will be evaluated on correctness, clarity, and structure. Correctness means your DataFrame operations and summaries reflect the intended logic and your validation checks pass. Clarity means your code is readable, with descriptive variable names and clean pandas usage. Structure means the notebook runs cleanly from top to bottom with each task completed in order and with visible outputs.
