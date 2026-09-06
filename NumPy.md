# 📅 NumPy

**Date:** September 6, 2026

Today, I learned about **NumPy**, a powerful Python library used for numerical computing and widely used in **Data Science and Machine Learning**.

## 🧠 What I Learned

### 1. NumPy Arrays

NumPy provides the `ndarray` data structure for working efficiently with numerical data.

```python
import numpy as np

numbers = np.array([10, 20, 30, 40, 50])
```

I also learned how to create **2D arrays**:

```python
matrix = np.array([
    [1, 2, 3],
    [4, 5, 6]
])
```

### 2. Array Properties

NumPy arrays provide useful properties to understand their structure:

```python
array.shape
array.ndim
array.size
array.dtype
```

* `shape` → dimensions of the array
* `ndim` → number of dimensions
* `size` → total number of elements
* `dtype` → data type of the elements

### 3. Indexing and Slicing

I learned how to access individual elements and portions of an array.

```python
numbers[0]
numbers[-1]
numbers[1:4]
```

For 2D arrays:

```python
matrix[0, 1]
```

### 4. Array Operations

One important feature of NumPy is that mathematical operations can be performed directly on entire arrays.

```python
numbers + 10
numbers * 2
numbers / 2
numbers ** 2
```

### 5. Statistical Functions

I learned useful NumPy functions for analysing numerical data:

```python
np.mean()
np.median()
np.min()
np.max()
np.sum()
np.std()
```

### 6. Creating Arrays

NumPy provides several functions for generating arrays:

```python
np.zeros()
np.ones()
np.arange()
np.linspace()
```

Example:

```python
np.arange(0, 10, 2)
```

#AI #MachineLearning #NumPy #Python #DataScience #AIJourney #MLJourney #LearningAI #PythonProgramming
