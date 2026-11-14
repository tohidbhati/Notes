# NUMPY – Complete Practical Notes
## Data Analytics Course

---

# 1. Introduction to NumPy

NumPy stands for **Numerical Python**.

It is a Python library used for:
- Numerical calculations
- Working with multidimensional arrays
- Mathematical operations
- Statistical calculations
- Data manipulation
- Scientific computing

### Why NumPy?

Python lists can store multiple values, but NumPy arrays are designed for efficient numerical operations.

### Installing NumPy

```bash
pip install numpy
```

### Importing NumPy

```python
import numpy as np
```

`np` is the standard alias used for NumPy.

---

# 2. Python List vs NumPy Array

### Python List

```python
marks = [70, 80, 90, 60]

print(marks)
print(type(marks))
```

### NumPy Array

```python
import numpy as np

marks = np.array([70, 80, 90, 60])

print(marks)
print(type(marks))
```

### Mathematical Difference

```python
# Python list
a = [10, 20, 30]
print(a * 2)

# NumPy array
b = np.array([10, 20, 30])
print(b * 2)
```

Output:

```text
[10, 20, 30, 10, 20, 30]

[20 40 60]
```

**Important:** Python list multiplication repeats the list, whereas NumPy multiplication performs element-wise multiplication.

---

# 3. Creating NumPy Arrays

## 3.1 One-Dimensional Array

```python
import numpy as np

arr = np.array([10, 20, 30, 40, 50])

print(arr)
```

## 3.2 Two-Dimensional Array

```python
arr = np.array([
    [10, 20, 30],
    [40, 50, 60]
])

print(arr)
```

## 3.3 Three-Dimensional Array

```python
arr = np.array([
    [[1, 2], [3, 4]],
    [[5, 6], [7, 8]]
])

print(arr)
```

## 3.4 Array of Zeros

```python
arr = np.zeros(5)

print(arr)
```

Output:

```text
[0. 0. 0. 0. 0.]
```

## 3.5 Array of Ones

```python
arr = np.ones(5)

print(arr)
```

## 3.6 Array with a Specific Value

```python
arr = np.full(5, 100)

print(arr)
```

Output:

```text
[100 100 100 100 100]
```

## 3.7 Using arange()

Creates evenly spaced values using a step size.

```python
arr = np.arange(1, 11)

print(arr)
```

Output:

```text
[1 2 3 4 5 6 7 8 9 10]
```

With step size:

```python
arr = np.arange(0, 20, 2)

print(arr)
```

Output:

```text
[0 2 4 6 8 10 12 14 16 18]
```

## 3.8 Using linspace()

Creates a specified number of evenly spaced values.

```python
arr = np.linspace(0, 100, 5)

print(arr)
```

Output:

```text
[  0.  25.  50.  75. 100.]
```

## 3.9 Identity Matrix

```python
arr = np.eye(3)

print(arr)
```

---

# 4. NumPy Array Properties

Consider:

```python
arr = np.array([
    [10, 20, 30],
    [40, 50, 60]
])
```

### 4.1 Number of Dimensions

```python
print(arr.ndim)
```

Output: `2`

### 4.2 Array Shape

```python
print(arr.shape)
```

Output: `(2, 3)`

It means 2 rows and 3 columns.

### 4.3 Total Number of Elements

```python
print(arr.size)
```

Output: `6`

### 4.4 Data Type

```python
print(arr.dtype)
```

### 4.5 Memory Size

```python
print(arr.itemsize)
```

Returns the memory occupied by each element in bytes.

---

# 5. NumPy Data Types

NumPy supports different numerical data types.

| Data Type | Description |
|---|---|
| int32 | 32-bit integer |
| int64 | 64-bit integer |
| float32 | 32-bit decimal |
| float64 | 64-bit decimal |
| bool_ | Boolean values |
| complex128 | Complex numbers |

### Example

```python
arr = np.array([10, 20, 30], dtype=np.float64)

print(arr)
print(arr.dtype)
```

### Type Conversion

```python
arr = np.array([10.5, 20.8, 30.2])

new_arr = arr.astype(int)

print(new_arr)
```

Output:

```text
[10 20 30]
```

---

# 6. NumPy Indexing

Indexing means accessing individual elements.

```python
arr = np.array([10, 20, 30, 40, 50])

print(arr[0])
print(arr[2])
print(arr[-1])
```

Output:

```text
10
30
50
```

## 6.1 Two-Dimensional Indexing

```python
arr = np.array([
    [10, 20, 30],
    [40, 50, 60]
])

print(arr[0, 0])
print(arr[0, 2])
print(arr[1, 1])
```

Output:

```text
10
30
50
```

---

# 7. NumPy Slicing

Slicing extracts a portion of an array.

Syntax:

```python
array[start:stop:step]
```

Example:

```python
arr = np.array([10, 20, 30, 40, 50, 60])

print(arr[1:4])
print(arr[:3])
print(arr[2:])
print(arr[::2])
```

Output:

```text
[20 30 40]
[10 20 30]
[30 40 50 60]
[10 30 50]
```

### Two-Dimensional Slicing

```python
arr = np.array([
    [10, 20, 30],
    [40, 50, 60],
    [70, 80, 90]
])

print(arr[0:2, 0:2])
```

Output:

```text
[[10 20]
 [40 50]]
```

---

# 8. Reshaping Arrays

Reshaping changes the dimensions of an array without changing its elements.

```python
arr = np.arange(1, 13)

new_arr = arr.reshape(3, 4)

print(new_arr)
```

Output:

```text
[[ 1  2  3  4]
 [ 5  6  7  8]
 [ 9 10 11 12]]
```

### Flattening

Converts a multidimensional array into a one-dimensional array.

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(arr.flatten())
```

---

# 9. Arithmetic Operations

NumPy supports element-wise mathematical operations.

```python
a = np.array([10, 20, 30])
b = np.array([2, 4, 5])

print(a + b)
print(a - b)
print(a * b)
print(a / b)
print(a ** 2)
```

Output:

```text
[12 24 35]
[ 8 16 25]
[ 20  80 150]
[5. 5. 6.]
[100 400 900]
```

### Mathematical Functions

```python
arr = np.array([1, 4, 9, 16, 25])

print(np.sqrt(arr))
print(np.square(arr))
print(np.power(arr, 2))
print(np.abs([-10, -20, 30]))
```

---

# 10. Statistical Operations

Statistics is an important part of data analytics.

Consider student marks:

```python
marks = np.array([70, 80, 90, 60, 85, 95])
```

### Sum

```python
print(np.sum(marks))
```

### Mean

```python
print(np.mean(marks))
```

### Median

```python
print(np.median(marks))
```

### Minimum

```python
print(np.min(marks))
```

### Maximum

```python
print(np.max(marks))
```

### Standard Deviation

```python
print(np.std(marks))
```

### Variance

```python
print(np.var(marks))
```

### Percentile

```python
print(np.percentile(marks, 75))
```

### Sorting

```python
print(np.sort(marks))
```

---

# 11. Broadcasting

Broadcasting allows NumPy to perform operations between arrays of compatible shapes.

### Example 1: Scalar Broadcasting

```python
arr = np.array([10, 20, 30])

print(arr + 5)
```

Output:

```text
[15 25 35]
```

### Example 2: Array Broadcasting

```python
a = np.array([
    [10, 20, 30],
    [40, 50, 60]
])

b = np.array([1, 2, 3])

print(a + b)
```

Output:

```text
[[11 22 33]
 [41 52 63]]
```

---

# 12. Filtering and Conditional Operations

Filtering helps extract data based on conditions.

```python
marks = np.array([45, 60, 75, 30, 90, 85])

passed = marks[marks >= 40]

print(passed)
```

Output:

```text
[45 60 75 90 85]
```

### Multiple Conditions

```python
marks = np.array([45, 60, 75, 30, 90, 85])

result = marks[(marks >= 50) & (marks <= 80)]

print(result)
```

### Using np.where()

```python
marks = np.array([35, 80, 45, 90, 25])

result = np.where(marks >= 40, "Pass", "Fail")

print(result)
```

### Counting Conditions

```python
print(np.count_nonzero(marks >= 40))
```

---

# 13. Joining and Splitting Arrays

## Concatenate

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

result = np.concatenate((a, b))

print(result)
```

## Vertical Stack

```python
a = np.array([1, 2])
b = np.array([3, 4])

print(np.vstack((a, b)))
```

## Horizontal Stack

```python
print(np.hstack((a, b)))
```

## Splitting

```python
arr = np.array([10, 20, 30, 40, 50, 60])

result = np.split(arr, 3)

print(result)
```

---

# 14. Random Numbers

NumPy provides random number generation.

```python
# Random integer
print(np.random.randint(1, 100))

# Random decimal
print(np.random.rand(5))

# Random normal distribution
print(np.random.randn(5))
```

### Reproducible Random Data

```python
np.random.seed(42)

print(np.random.randint(1, 100, 5))
```

For new code, the recommended approach is:

```python
rng = np.random.default_rng(42)

print(rng.integers(1, 100, size=5))
```

---

# 15. File Handling with NumPy

NumPy can read and write numerical data files.

## 15.1 Saving an Array

```python
arr = np.array([10, 20, 30, 40, 50])

np.save("marks.npy", arr)
```

## 15.2 Loading an Array

```python
data = np.load("marks.npy")

print(data)
```

## 15.3 Saving as Text File

```python
arr = np.array([10, 20, 30, 40, 50])

np.savetxt("marks.txt", arr)
```

## 15.4 Loading Text File

```python
data = np.loadtxt("marks.txt")

print(data)
```

## 15.5 Working with CSV Files

Create a file named `students.csv`:

```csv
Name,Python,SQL,Statistics
Amit,85,78,90
Rahul,70,65,75
Priya,95,88,92
Neha,60,72,68
```

Read numerical columns using NumPy:

```python
data = np.loadtxt(
    "students.csv",
    delimiter=",",
    skiprows=1,
    usecols=(1, 2, 3)
)

print(data)
```

Calculate average marks:

```python
average = np.mean(data, axis=1)

print(average)
```

Calculate subject-wise average:

```python
subject_average = np.mean(data, axis=0)

print(subject_average)
```

**Note:** NumPy is most suitable for numerical data. For mixed data containing names, dates and numbers, Pandas is generally more convenient.

---

# 16. NumPy with Pandas

Pandas is a Python library used for data manipulation and analysis.

NumPy and Pandas work together frequently.

### Installation

```bash
pip install pandas
```

### Importing

```python
import numpy as np
import pandas as pd
```

## Example: Student Performance

```python
data = {
    "Name": ["Amit", "Rahul", "Priya", "Neha"],
    "Python": [85, 70, 95, 60],
    "SQL": [78, 65, 88, 72],
    "Statistics": [90, 75, 92, 68]
}

df = pd.DataFrame(data)

print(df)
```

### Convert Pandas Columns into NumPy Arrays

```python
python_marks = df["Python"].to_numpy()

print(python_marks)
```

### Calculate Average Using NumPy

```python
marks = df[["Python", "SQL", "Statistics"]].to_numpy()

df["Average"] = np.mean(marks, axis=1)

print(df)
```

### Calculate Highest Marks

```python
df["Highest"] = np.max(marks, axis=1)

print(df)
```

### Find Students Who Passed

```python
df["Result"] = np.where(df["Average"] >= 40, "Pass", "Fail")

print(df)
```

### Find Topper

```python
topper = df.loc[df["Average"].idxmax()]

print(topper)
```

### Export Result

```python
df.to_csv("student_results.csv", index=False)
```

---

# 17. NumPy with Matplotlib

Matplotlib is used for data visualization.

NumPy helps prepare numerical data, while Matplotlib displays it graphically.

### Installation

```bash
pip install matplotlib
```

### Importing

```python
import numpy as np
import matplotlib.pyplot as plt
```

## 17.1 Line Chart

```python
months = np.array(["Jan", "Feb", "Mar", "Apr", "May"])

sales = np.array([10000, 15000, 12000, 18000, 25000])

plt.plot(months, sales, marker="o")

plt.title("Monthly Sales")
plt.xlabel("Months")
plt.ylabel("Sales")

plt.show()
```

## 17.2 Bar Chart

```python
students = np.array(["Amit", "Rahul", "Priya", "Neha"])

marks = np.array([85, 70, 95, 60])

plt.bar(students, marks)

plt.title("Student Marks")
plt.xlabel("Students")
plt.ylabel("Marks")

plt.show()
```

## 17.3 Pie Chart

```python
subjects = ["Python", "SQL", "Statistics"]

marks = np.array([85, 75, 90])

plt.pie(
    marks,
    labels=subjects,
    autopct="%1.1f%%"
)

plt.title("Subject-wise Marks Distribution")

plt.show()
```

## 17.4 Histogram

```python
marks = np.array([
    45, 50, 55, 60, 65,
    70, 75, 80, 85, 90,
    95, 40, 60, 70, 80
])

plt.hist(marks, bins=5, edgecolor="black")

plt.title("Marks Distribution")
plt.xlabel("Marks")
plt.ylabel("Number of Students")

plt.show()
```

## 17.5 Scatter Plot

```python
study_hours = np.array([1, 2, 3, 4, 5, 6])

marks = np.array([35, 45, 55, 65, 75, 90])

plt.scatter(study_hours, marks)

plt.title("Study Hours vs Marks")
plt.xlabel("Study Hours")
plt.ylabel("Marks")

plt.show()
```

## 17.6 Multiple Lines

```python
months = np.array([1, 2, 3, 4, 5])

sales_2025 = np.array([10000, 15000, 12000, 18000, 20000])

sales_2026 = np.array([12000, 17000, 16000, 22000, 26000])

plt.plot(months, sales_2025, marker="o", label="2025")

plt.plot(months, sales_2026, marker="o", label="2026")

plt.title("Sales Comparison")

plt.xlabel("Months")
plt.ylabel("Sales")

plt.legend()

plt.show()
```

---

# 18. Mini Project: Student Performance Analysis

## Objective

Analyze student marks using NumPy, Pandas and Matplotlib.

### Step 1: Import Libraries

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

### Step 2: Create Dataset

```python
data = {
    "Name": [
        "Amit", "Rahul", "Priya", "Neha",
        "Karan", "Simran", "Vikas", "Anjali"
    ],

    "Python": [85, 70, 95, 60, 75, 88, 55, 92],

    "SQL": [78, 65, 88, 72, 80, 90, 60, 85],

    "Statistics": [90, 75, 92, 68, 85, 87, 65, 95]
}

df = pd.DataFrame(data)

print(df)
```

### Step 3: Calculate Total and Average

```python
subjects = ["Python", "SQL", "Statistics"]

marks = df[subjects].to_numpy()

df["Total"] = np.sum(marks, axis=1)

df["Average"] = np.mean(marks, axis=1)

print(df)
```

### Step 4: Assign Grades

```python
df["Grade"] = np.select(
    [
        df["Average"] >= 90,
        df["Average"] >= 80,
        df["Average"] >= 70,
        df["Average"] >= 60,
        df["Average"] >= 40
    ],
    [
        "A+",
        "A",
        "B",
        "C",
        "D"
    ],
    default="F"
)

print(df)
```

### Step 5: Find Topper

```python
topper = df.loc[df["Total"].idxmax()]

print("Class Topper:")
print(topper)
```

### Step 6: Calculate Subject Averages

```python
subject_avg = np.mean(marks, axis=0)

print(subject_avg)
```

### Step 7: Visualize Subject Averages

```python
plt.bar(subjects, subject_avg)

plt.title("Average Marks by Subject")
plt.xlabel("Subjects")
plt.ylabel("Average Marks")

plt.show()
```

### Step 8: Compare Student Performance

```python
plt.bar(df["Name"], df["Average"])

plt.title("Student Performance Comparison")

plt.xlabel("Students")
plt.ylabel("Average Marks")

plt.xticks(rotation=45)

plt.show()
```

### Step 9: Save Final Results

```python
df.to_csv("final_student_analysis.csv", index=False)

print("Analysis completed successfully!")
```

---

# 19. Practice Questions

## Beginner Level

1. Create a NumPy array containing numbers from 1 to 20.
2. Create an array of 10 zeros.
3. Create an array of 10 ones.
4. Find the maximum and minimum values.
5. Calculate the mean and median.
6. Extract the first five elements from an array.
7. Reverse an array.
8. Convert a one-dimensional array into a 3x3 matrix.

## Intermediate Level

1. Create an array of 20 random integers.
2. Find all values greater than 50.
3. Count the number of even numbers.
4. Replace values below 40 with zero.
5. Calculate row-wise and column-wise averages.
6. Combine two arrays using concatenate().
7. Split an array into four equal parts.
8. Calculate standard deviation and variance.

## Advanced Level

1. Create a 5x5 random matrix.
2. Find the maximum value in every row.
3. Normalize an array using min-max normalization.
4. Calculate the correlation between two numerical arrays.
5. Generate a dataset and identify outliers using the IQR method.
6. Load a CSV file and perform statistical analysis.
7. Combine NumPy, Pandas and Matplotlib to analyze a dataset.

---

# 20. Important NumPy Functions Cheat Sheet

| Function | Purpose |
|---|---|
| np.array() | Create an array |
| np.zeros() | Create zero array |
| np.ones() | Create one array |
| np.full() | Create filled array |
| np.arange() | Generate range |
| np.linspace() | Generate evenly spaced values |
| np.reshape() | Change array shape |
| np.flatten() | Convert to 1D |
| np.concatenate() | Join arrays |
| np.split() | Split arrays |
| np.mean() | Calculate average |
| np.median() | Calculate median |
| np.sum() | Calculate sum |
| np.min() | Find minimum |
| np.max() | Find maximum |
| np.std() | Standard deviation |
| np.var() | Variance |
| np.sort() | Sort elements |
| np.where() | Conditional selection |
| np.unique() | Find unique values |
| np.sqrt() | Square root |
| np.percentile() | Calculate percentile |
| np.loadtxt() | Read numerical text/CSV data |
| np.savetxt() | Save numerical text data |
| np.save() | Save NumPy binary file |
| np.load() | Load NumPy binary file |

---

# Conclusion

NumPy is an essential library in the Data Analytics ecosystem.

It provides efficient numerical calculations and works closely with:

- **Pandas:** Data manipulation and analysis.
- **Matplotlib:** Data visualization.
- **SQL:** Data extraction from relational databases.

A typical data analytics workflow:

1. Extract data using SQL.
2. Load and clean data using Pandas.
3. Perform numerical calculations using NumPy.
4. Visualize insights using Matplotlib.
5. Communicate findings through reports.

**End of NumPy Notes**
