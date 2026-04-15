# Module 6 — Exploratory Data Analysis with Pandas

**Session Time:** 120 minutes

---

## Prerequisites

- Python fundamentals (variables, conditionals, functions)  
- NumPy basics (arrays, vectorised operations)  
- Pandas fundamentals (loading, cleaning, transforming data)  
- Completion of **Module 5 — Pandas Fundamentals: Data Wrangling**

---

## Session Breakdown

| Segment | Topic                                      | Duration (minutes) |
|--------:|--------------------------------------------|--------------------|
| 1       | Introduction to Exploratory Data Analysis  | 10                 |
| 2       | Filtering & Selecting Data (`.loc[]`)      | 15                 |
| 3       | Descriptive Statistics with Pandas         | 15                 |
| 4       | Grouping and Aggregation (`.groupby()`)    | 20                 |
| 5       | Cleaning Columns (`.rename()`, `.drop()`)  | 10                 |
| 6       | Identifying Patterns and Anomalies         | 20                 |
| 7       | Bridge to NumPy (Arrays & Vectorization)   | 10                 |
|         | **Lab — Optimising Calculations with NumPy Arrays** | **20**     |

---

## Learning Objectives

By the end of this module, you'll be able to:

- Filter and subset data using Pandas  
- Use `.loc[]` to safely select and modify data  
- Perform exploratory data analysis using Pandas DataFrames  
- Group and aggregate data using `.groupby()`  
- Clean and restructure datasets using `.rename()` and `.drop()`  
- Identify trends, patterns, and anomalies  
- Understand how Pandas connects to NumPy for numerical computation  

---

## What You Will Learn

In this module, you move from **clean data** to **insight-ready data**.

You’ll use Pandas to:
- Filter and subset relevant data  
- Summarise datasets  
- Compare groups  
- Prepare clean outputs for downstream analysis  

Exploratory Data Analysis (EDA) is a critical step because it helps you:

- Validate assumptions  
- Detect unexpected behaviour  
- Identify patterns  
- Reduce downstream errors  

---

## Introduction to Exploratory Data Analysis (EDA)

EDA focuses on **understanding your dataset before drawing conclusions**.

Key questions include:

- What does “typical” look like?
- Are there unusual values?
- How do groups compare?
- Does the data behave as expected?

---

## Filtering and Selecting Data with `.loc[]`

Filtering allows you to focus on relevant subsets of your data.

```python
over_10k = df['price'] > 10_000
df.loc[over_10k]
```

You can combine multiple conditions:

```python
carat_lt5 = df['carat'] < 5
ideal_cut = df['cut'] == 'Ideal'

df.loc[carat_lt5 & ideal_cut]
```

> Build conditions using `df['col']`, then apply them using `.loc[]`

---

## Grouping and Aggregation with `.groupby()`

```python
df.groupby('cut')['price'].mean()
```

```python
df.groupby('cut')['price'].agg(['mean', 'min', 'max'])
```

---

## Cleaning and Restructuring Data

```python
df = df.rename(columns={'price': 'diamond_price'})
df = df.drop(columns=['x', 'y', 'z'])
```

---

## Bridging Pandas to NumPy

```python
df['price'].to_numpy()
```

```python
import numpy as np

arr = np.arange(1, 6)
arr * 2
```

---

## Summary

> Use **Pandas** to explore and manipulate data.  
> Use **NumPy** to perform fast numerical operations on that data.
