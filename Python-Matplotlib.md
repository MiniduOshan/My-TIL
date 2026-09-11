# 📊 TIL — Matplotlib

**Date:** 2026-09-11

## What I Learned

Today I learned the basics of **Matplotlib**, a Python library used to create charts and visualizations.

### 🔹 Basic Line Plot

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]

plt.plot(x, y)
plt.show()
```

### 🔹 Adding a Title and Labels

```python
plt.plot(x, y)

plt.title("Simple Line Chart")
plt.xlabel("X Values")
plt.ylabel("Y Values")

plt.show()
```

### 🔹 Bar Chart

```python
categories = ["A", "B", "C"]
values = [10, 20, 15]

plt.bar(categories, values)
plt.show()
```

### 🔹 Scatter Plot

```python
plt.scatter(x, y)
plt.show()
```

## Key Points

* `matplotlib.pyplot` is commonly imported as `plt`.
* `plt.plot()` creates a line chart.
* `plt.bar()` creates a bar chart.
* `plt.scatter()` creates a scatter plot.
* `plt.title()` adds a title.
* `plt.xlabel()` and `plt.ylabel()` add axis labels.
* `plt.show()` displays the chart.

## Why Matplotlib Is Useful for AI/ML

Matplotlib is useful for visualizing data and understanding machine learning results.

It can be used to visualize:

* Data distributions
* Trends and patterns
* Model performance
* Training and validation results
* Predictions vs actual values
* Correlations between variables

## Today's Takeaway

**Matplotlib helps turn numerical data into visual information, making patterns and results easier to understand.**
