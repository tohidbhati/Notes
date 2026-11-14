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

### Theory (in simple words)

Think of NumPy as a **powerful calculator for lists of numbers**. Normal Python is good at general tasks, but it is slow when you have thousands or millions of numbers to calculate. NumPy solves this by giving us a special container called an **array** (officially `ndarray`, meaning "n-dimensional array") that stores numbers in a tight, organized way in memory.

Under the hood, NumPy is written in the C language, so calculations run much faster than normal Python loops. Almost every data analytics library (Pandas, Matplotlib, Scikit-learn) is built on top of NumPy, so learning it first makes everything else easier.

### Why NumPy?

Python lists can store multiple values, but NumPy arrays are designed for efficient numerical operations.

**Key advantages:**
- **Fast:** operations on whole arrays happen in one go, without writing loops.
- **Less memory:** all elements share one data type, so storage is compact.
- **Easy math:** you can add, multiply or compare entire arrays with one line.
- **Rich tools:** built-in functions for statistics, sorting, random numbers and more.

### Installing NumPy

```bash
pip install numpy
```

### Importing NumPy

```python
import numpy as np
```

`np` is the standard alias used for NumPy. An alias is just a short nickname, so we write `np.array()` instead of `numpy.array()`.

---

# 2. Python List vs NumPy Array

### Theory (in simple words)

A **Python list** is like a flexible bag: it can hold numbers, text, and even other lists mixed together. This flexibility makes it slower for math.

A **NumPy array** is like a neat row of boxes where **every box holds the same type of data** (all integers, or all decimals). Because of this rule, NumPy knows exactly how to calculate quickly.

The biggest practical difference is how operators behave:
- On a list, `*` means "repeat the list".
- On a NumPy array, `*` means "multiply each number".

| Feature | Python List | NumPy Array |
|---|---|---|
| Data types | Can be mixed | Same type only |
| Speed | Slower | Much faster |
| Math on whole data | Needs loops | Works directly |
| Memory use | More | Less |

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

### Theory (in simple words)

Before we can analyze data, we need to put it into an array. NumPy gives us many ways to do this:
- **Manually**, by passing a list to `np.array()`.
- **Automatically**, using helper functions like `zeros`, `ones`, `arange` and `linspace` when we need ready-made arrays.

**Dimensions explained:**
- **1D array** = a single row of numbers (like a list). Example: marks of one student.
- **2D array** = rows and columns (like an Excel sheet or table). Example: marks of many students in many subjects.
- **3D array** = a stack of 2D tables (like multiple Excel sheets). Example: marks of the same class across several years.

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

Useful when you need a blank array that you will fill later.

```python
arr = np.zeros(5)

print(arr)
```

Output:

```text
[0. 0. 0. 0. 0.]
```

## 3.5 Array of Ones

Same idea as zeros, but filled with 1.

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

Creates evenly spaced values using a **step size**. It works like Python's `range()`, but returns a NumPy array. The stop value is **not included**.

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

Creates a **specified number of** evenly spaced values. The difference from `arange()`:
- `arange()` → you decide the **step size**.
- `linspace()` → you decide **how many values** you want, and the **end value is included**.

```python
arr = np.linspace(0, 100, 5)

print(arr)
```

Output:

```text
[  0.  25.  50.  75. 100.]
```

## 3.9 Identity Matrix

An identity matrix has 1s on the diagonal and 0s everywhere else. It is used in matrix mathematics.

```python
arr = np.eye(3)

print(arr)
```

---

# 4. NumPy Array Properties

### Theory (in simple words)

Every array carries some "information labels" about itself, called **attributes**. They tell us what the array looks like without having to print all the data. This is very useful when working with large datasets, where you cannot read every number.

Consider:

```python
arr = np.array([
    [10, 20, 30],
    [40, 50, 60]
])
```

### 4.1 Number of Dimensions

How many "directions" the array has (1D, 2D, 3D).

```python
print(arr.ndim)
```

Output: `2`

### 4.2 Array Shape

The size of the array in each direction, written as `(rows, columns)`.

```python
print(arr.shape)
```

Output: `(2, 3)`

It means 2 rows and 3 columns.

### 4.3 Total Number of Elements

Rows × columns = total values.

```python
print(arr.size)
```

Output: `6`

### 4.4 Data Type

The kind of data stored (integer, decimal, etc.).

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

### Theory (in simple words)

Since every element in an array must be the same type, NumPy needs to know **what type** of data it is storing. The number in the name (32, 64) tells how many **bits** of memory each value uses:
- More bits = can store bigger numbers or more decimal accuracy, but uses more memory.
- Fewer bits = saves memory, but has limits.

For most beginner work, NumPy chooses a suitable type automatically (`int64` for whole numbers, `float64` for decimals).

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

`astype()` changes an array from one type to another. Converting decimals to integers **cuts off** the decimal part (it does not round).

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

### Theory (in simple words)

**Indexing** means picking one specific value from an array using its **position number**, just like finding a house using its address.

Two important rules:
1. **Counting starts from 0**, not 1. So the first element is at position `0`.
2. **Negative index counts from the end.** `-1` is the last element, `-2` is the second last, and so on.

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

In a 2D array, you need **two addresses**: `[row, column]`.

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

### Theory (in simple words)

If indexing picks **one** value, **slicing** picks a **range** of values, like cutting a slice from a cake.

The syntax has three parts: `start : stop : step`
- **start** → where to begin (included)
- **stop** → where to end (**not included**)
- **step** → how many positions to jump each time

If you leave a part empty, NumPy uses a default: start = beginning, stop = end, step = 1.

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

For 2D arrays, give one slice for rows and one for columns: `[row_slice, column_slice]`.

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

**Tip:** A slice is a *view* of the original array, not a separate copy. Changing the slice can change the original array. Use `.copy()` if you want an independent copy.

---

# 8. Reshaping Arrays

### Theory (in simple words)

**Reshaping** means rearranging the same numbers into a different layout, like taking 12 chocolates from a single row and arranging them into 3 rows of 4.

The only rule: **the total number of elements must stay the same.** 12 elements can become 3×4, 4×3, 2×6 and so on, but not 5×3 (that needs 15).

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

**Shortcut:** Use `-1` to let NumPy calculate one dimension for you. For example, `arr.reshape(3, -1)` automatically becomes 3 rows × 4 columns.

### Flattening

Flattening is the opposite of reshaping into a table: it **converts a multidimensional array into a one-dimensional array**.

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(arr.flatten())
```

---

# 9. Arithmetic Operations

### Theory (in simple words)

In NumPy, arithmetic works **element by element**. When you add two arrays, the first number is added to the first number, the second to the second, and so on. This is called **element-wise operation**.

This replaces the need for loops. Instead of writing a loop to add 1000 pairs of numbers, one line `a + b` does it all.

**Requirement:** The two arrays should have the same shape (or compatible shapes, see Broadcasting in Section 11).

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

NumPy also provides ready-made math functions that apply to every element.

```python
arr = np.array([1, 4, 9, 16, 25])

print(np.sqrt(arr))
print(np.square(arr))
print(np.power(arr, 2))
print(np.abs([-10, -20, 30]))
```

- `sqrt` → square root
- `square` → number multiplied by itself
- `power` → raise to any power
- `abs` → absolute value (removes the negative sign)

---

# 10. Statistical Operations

### Theory (in simple words)

Statistics means **summarizing lots of data using a few meaningful numbers**. Instead of reading 1000 marks, we can say "the average is 78". NumPy has built-in functions for this, which makes it a core tool in data analytics.

**What each measure means:**

| Measure | Simple meaning |
|---|---|
| **Sum** | Add everything together |
| **Mean** | The average: sum ÷ count |
| **Median** | The middle value after sorting. Not affected much by extreme values |
| **Min / Max** | Smallest / largest value |
| **Variance** | How spread out the numbers are from the average (in squared units) |
| **Standard deviation** | Spread of data in the same units as the data. Small = values are close to average; large = values are scattered |
| **Percentile** | The value below which a given percentage of data falls. 75th percentile = 75% of values are below it |

**Mean vs Median:** If salaries are 20k, 22k, 25k and 500k, the mean is pulled up by the big value, while the median stays closer to a "typical" salary.

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

### The `axis` parameter (important for 2D data)

In a 2D array, you can choose the direction of calculation:
- `axis=0` → calculate **down the columns** (one result per column).
- `axis=1` → calculate **across the rows** (one result per row).

---

# 11. Broadcasting

### Theory (in simple words)

Normally, to add two arrays they must be the same size. **Broadcasting** is NumPy's smart feature that **automatically stretches the smaller array** so the operation can still happen. You do not need to copy or repeat data yourself.

Two common situations:
1. **Scalar with array:** a single number is applied to every element.
2. **Small array with big array:** the small array is repeated across the rows (or columns) of the bigger one.

**Rule of thumb:** Compare shapes from the right side. Two dimensions are compatible if they are **equal**, or **one of them is 1** (or missing).

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

Here `b` (shape 3) is stretched across both rows of `a` (shape 2×3).

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

**Real-life use:** Adding a 5-mark bonus to every student, or converting a whole price column to a different currency with one multiplication.

---

# 12. Filtering and Conditional Operations

### Theory (in simple words)

**Filtering** means keeping only the data that meets a condition, like selecting only students who scored 40 or more.

It works in two steps:
1. NumPy applies the condition to every element and produces a list of **True / False** values (called a *boolean mask*).
2. When you put that mask inside the square brackets, NumPy keeps only the elements marked **True**.

For multiple conditions, use:
- `&` for **AND** (both must be true)
- `|` for **OR** (at least one must be true)
- `~` for **NOT**

**Important:** Always put each condition inside **brackets ( )** when combining them. Do not use Python's `and` / `or` with arrays; they will cause an error.

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

`np.where(condition, value_if_true, value_if_false)` works like an **if-else for the whole array**. It does not remove anything; it replaces values based on the condition.

```python
marks = np.array([35, 80, 45, 90, 25])

result = np.where(marks >= 40, "Pass", "Fail")

print(result)
```

### Counting Conditions

Since `True` counts as 1 and `False` as 0, we can count how many values meet a condition.

```python
print(np.count_nonzero(marks >= 40))
```

---

# 13. Joining and Splitting Arrays

### Theory (in simple words)

Sometimes data comes in pieces and needs to be combined, or one big array needs to be divided into parts.

- **Joining** = attaching arrays together, like connecting train coaches.
- **Splitting** = cutting one array into smaller arrays.

**Which join to use?**

| Function | What it does |
|---|---|
| `concatenate` | Joins arrays end to end along an existing direction |
| `vstack` | Stacks arrays **vertically** (one below another, adding rows) |
| `hstack` | Stacks arrays **horizontally** (side by side, adding columns) |

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

`np.split(arr, 3)` divides the array into **3 equal parts**. The array length must be divisible by the number of parts, otherwise NumPy gives an error (use `np.array_split()` for unequal parts).

```python
arr = np.array([10, 20, 30, 40, 50, 60])

result = np.split(arr, 3)

print(result)
```

---

# 14. Random Numbers

### Theory (in simple words)

Random numbers are used to **create sample data, simulate situations, and shuffle or pick samples**. When you are learning, you do not always have a real dataset, so random numbers help you practice.

Computers do not produce truly random numbers; they follow a mathematical formula that *looks* random. This is called **pseudo-random**. Because it is formula-based, we can control it using a **seed**.

**Seed:** A starting number for the formula. Using the same seed gives the **same random numbers every time**, which is important when you want your results to be repeatable (for example, when sharing your work or testing).

**Main functions:**
- `randint(low, high)` → random whole numbers (the high value is not included).
- `rand()` → random decimals between 0 and 1, evenly spread.
- `randn()` → random decimals from the **normal distribution** (bell curve), centered around 0. Values can be negative.

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

### Theory (in simple words)

Real-world data lives in **files**, not typed inside code. File handling means **saving** your arrays so you can use them later, and **loading** data from files into arrays.

NumPy supports two kinds of files:
- **Binary files (`.npy`)**: NumPy's own format. Fast and exact, but you cannot read them in Notepad.
- **Text files (`.txt`, `.csv`)**: Human-readable and can be opened in Excel or Notepad, but slightly slower.

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

**CSV** stands for *Comma-Separated Values*: a simple text file where each line is a row and commas separate the columns.

Create a file named `students.csv`:

```csv
Name,Python,SQL,Statistics
Amit,85,78,90
Rahul,70,65,75
Priya,95,88,92
Neha,60,72,68
```

Read numerical columns using NumPy:

- `delimiter=","` → tells NumPy that commas separate the values.
- `skiprows=1` → skips the header line (column names).
- `usecols=(1, 2, 3)` → reads only the number columns and ignores the Name column (since text would cause an error).

```python
data = np.loadtxt(
    "students.csv",
    delimiter=",",
    skiprows=1,
    usecols=(1, 2, 3)
)

print(data)
```

Calculate average marks (per student, so across each row):

```python
average = np.mean(data, axis=1)

print(average)
```

Calculate subject-wise average (per subject, so down each column):

```python
subject_average = np.mean(data, axis=0)

print(subject_average)
```

**Note:** NumPy is most suitable for numerical data. For mixed data containing names, dates and numbers, Pandas is generally more convenient.

---

# 16. NumPy with Pandas

### Theory (in simple words)

**Pandas** is a library for working with **tables of data**, like Excel sheets inside Python. Its main structure is the **DataFrame**: a table with rows, columns and column names. It can hold mixed data (text, numbers, dates).

How the two libraries differ and cooperate:
- **NumPy** = fast math on pure numbers.
- **Pandas** = organizing, labeling, cleaning and reading data tables.

In practice, Pandas stores its numeric data using NumPy underneath. You can pull the numbers out as a NumPy array (`to_numpy()`), do calculations, and put the results back as a new column.

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

A DataFrame can be created from a dictionary: each key becomes a column name, and each list becomes the column values.

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

Selecting several columns gives a table of numbers; `axis=1` calculates the average across each student's row.

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

`idxmax()` returns the row position of the highest value, and `loc` fetches that row.

```python
topper = df.loc[df["Average"].idxmax()]

print(topper)
```

### Export Result

```python
df.to_csv("student_results.csv", index=False)
```

`index=False` prevents Pandas from saving the extra row-number column.

---

# 17. NumPy with Matplotlib

### Theory (in simple words)

Numbers in tables are hard to understand quickly. A **chart** shows patterns instantly. **Matplotlib** is Python's most popular library for drawing charts and graphs.

NumPy prepares and calculates the numbers, and Matplotlib draws them.

**Choosing the right chart:**

| Chart | Best used for |
|---|---|
| **Line chart** | Showing change over time (trends) |
| **Bar chart** | Comparing categories |
| **Pie chart** | Showing parts of a whole (percentage share) |
| **Histogram** | Showing how data is distributed (how many values fall in each range) |
| **Scatter plot** | Showing the relationship between two numeric variables |

**Common commands used in every chart:**
- `plt.title()` → heading of the chart
- `plt.xlabel()` / `plt.ylabel()` → names of the axes
- `plt.legend()` → label box when there are multiple lines
- `plt.show()` → displays the chart

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

Points are connected by a line to show how something changes, such as sales across months.

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

Each category gets a bar; the taller the bar, the larger the value.

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

The circle is divided into slices; each slice shows a share of the total. `autopct` prints the percentage on each slice.

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

Groups values into ranges called **bins** and shows how many values fall in each bin. Unlike a bar chart, it is used for **continuous numeric data**.

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

Each dot is one observation, placed using two values (x and y). If dots rise from left to right, the two variables are positively related (more study hours → higher marks).

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

Drawing several lines on one chart makes comparison easy. The `label` and `legend()` tell which line is which.

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

### Theory (in simple words)

This project follows the **real workflow of a data analyst**:
1. **Collect** data (create the dataset).
2. **Calculate** new useful numbers (total, average).
3. **Categorize** (assign grades).
4. **Find insights** (topper, subject averages).
5. **Visualize** (charts).
6. **Share** (save results to a file).

Each library does what it is best at: Pandas holds the table, NumPy calculates, and Matplotlib draws.

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

Total = sum of all subjects for each student. Average = total ÷ number of subjects.

```python
subjects = ["Python", "SQL", "Statistics"]

marks = df[subjects].to_numpy()

df["Total"] = np.sum(marks, axis=1)

df["Average"] = np.mean(marks, axis=1)

print(df)
```

### Step 4: Assign Grades

`np.select()` is like a multi-level if-elif-else. It checks the conditions in order and gives the grade of the first one that is true. Anything that matches none gets the `default` grade.

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

This shows which subject the class is strongest or weakest in.

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

`rotation=45` tilts the names so they do not overlap.

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

### Theory (in simple words)

Reading is not enough to learn programming; **you learn by doing**. Try each question yourself first, then check the notes if you get stuck. The questions are arranged from easy to hard so your confidence builds step by step.

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
   *(Hint: new value = (x − min) ÷ (max − min), which scales all values between 0 and 1.)*
4. Calculate the correlation between two numerical arrays.
   *(Hint: correlation tells how strongly two variables move together. Try `np.corrcoef()`.)*
5. Generate a dataset and identify outliers using the IQR method.
   *(Hint: IQR = Q3 − Q1. Values below Q1 − 1.5×IQR or above Q3 + 1.5×IQR are outliers, meaning unusually small or large values.)*
6. Load a CSV file and perform statistical analysis.
7. Combine NumPy, Pandas and Matplotlib to analyze a dataset.

---

# 20. Important NumPy Functions Cheat Sheet

### Theory (in simple words)

A cheat sheet is a **quick-revision table**. You do not need to memorize everything; just remember what each function is *for*, and you can look up the exact usage when needed.

| Function | Purpose |
|---|---|
| np.array() | Create an array |
| np.zeros() | Create zero array |
| np.ones() | Create one array |
| np.full() | Create filled array |
| np.arange() | Generate range |
| np.linspace() | Generate evenly spaced values |
| np.reshape() | Change array shape |
| arr.flatten() | Convert to 1D (a method called on the array) |
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

### Quick Summary of Key Ideas

- A NumPy array holds **same-type numbers** and is **fast**.
- Operations are **element-wise**; no loops needed.
- **Indexing** picks one value; **slicing** picks a range; counting starts at 0.
- **Broadcasting** lets arrays of different sizes work together.
- **Filtering** uses True/False conditions to select data.
- `axis=0` works down **columns**; `axis=1` works across **rows**.
- NumPy calculates, Pandas organizes, Matplotlib visualizes.

**End of NumPy Notes**
