# NumPy – Complete Theory & Practical Notes

Data Analytics Course · Nov 15, 2026 · @Tohid

## 1. Introduction to NumPy

NumPy stands for **Numerical Python**. It is a Python library built for fast numerical work on large collections of numbers.

It is used for:

- Numerical calculations
- Working with multidimensional arrays
- Mathematical operations
- Statistical calculations
- Data manipulation
- Scientific computing

### 1.1 What is NumPy? (Theory)

Think of NumPy as a **powerful calculator for lists of numbers**. Normal Python is good at general tasks, but it becomes slow when you have thousands or millions of numbers to process. NumPy solves this by giving us a special container called an **array**. Its official name is `ndarray`, meaning "n-dimensional array".

The central idea is that an array stores numbers in one tight, organized block of memory. Every element has the same data type, so NumPy does not need to check the type of each value before calculating with it.

Under the hood, NumPy is written in **C**. When you write `a + b`, the loop that adds each pair of numbers runs in compiled C code, not in the slower Python interpreter. This style of working, where one operation is applied to a whole array at once, is called **vectorization**.

Almost every data analytics library (Pandas, Matplotlib, SciPy, Scikit-learn) is built on top of NumPy. Learning it first makes everything that follows easier.

### 1.2 Why NumPy?

Python lists can store multiple values, but NumPy arrays are designed specifically for efficient numerical operations.

**Key advantages:**

- **Fast:** operations on whole arrays happen in one go, without writing Python loops.
- **Less memory:** all elements share one data type, so storage is compact and predictable.
- **Easy math:** you can add, multiply or compare entire arrays with a single line.
- **Rich tools:** built-in functions for statistics, sorting, random numbers, linear algebra and more.

**Why is it faster? (Theory)**

- A Python list is a collection of *references*. Each item is a separate Python object stored somewhere in memory, and the list only remembers where to find them. Reading a million numbers means following a million references.
- A NumPy array stores the raw values side by side in **contiguous memory**. The processor can read them in order very quickly.
- Because the type is fixed, the same compiled instruction can be applied to every element.

### 1.3 Installing NumPy

`pip` is Python's package installer. This command downloads NumPy from the Python Package Index and installs it.

```bash
pip install numpy
```

### 1.4 Importing NumPy

Installing puts the library on your computer. Importing makes it available inside your program.

```python
import numpy as np
```

`np` is the standard alias used for NumPy. An alias is just a short nickname, so we write `np.array()` instead of `numpy.array()`. Almost every tutorial and project uses `np`, so following this convention makes your code easy for others to read.

## 2. Python List vs NumPy Array

### 2.1 Theory

A **Python list** is like a flexible bag: it can hold numbers, text, and even other lists mixed together. This flexibility is convenient, but it makes lists slower for mathematics, because Python has to check the type of every item before using it.

A **NumPy array** is like a neat row of boxes where **every box holds the same type of data** (all integers, or all decimals). Because of this rule, NumPy knows exactly how to calculate quickly, and it can store the values compactly.

The biggest *practical* difference is how operators behave:

- On a list, `*` means "repeat the list".
- On a NumPy array, `*` means "multiply each number".

The same operator therefore has a different meaning depending on the container. This is why you must be sure whether you are holding a list or an array before doing mathematics.

| Feature | Python List | NumPy Array |
| --- | --- | --- |
| Data types | Can be mixed | Same type only |
| Speed | Slower | Much faster |
| Math on whole data | Needs loops | Works directly |
| Memory use | More | Less |

### 2.2 Python List

```python
marks = [70, 80, 90, 60]

print(marks)
print(type(marks))
```

`type()` tells you what kind of object a variable holds. For a list it prints `<class 'list'>`.

### 2.3 NumPy Array

```python
import numpy as np

marks = np.array([70, 80, 90, 60])

print(marks)
print(type(marks))
```

`np.array()` converts a Python list into a NumPy array. Here `type()` prints `<class 'numpy.ndarray'>`, confirming it is an `ndarray`.

### 2.4 Mathematical Difference

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

**Reading the output:** a list prints with commas (`[10, 20, 30]`), while a NumPy array prints with spaces (`[20 40 60]`). This small difference helps you recognize which one you are looking at.

## 3. Creating NumPy Arrays

### 3.0 Theory

Before we can analyze data, we need to put it into an array. NumPy gives us two broad approaches:

- **Manually**, by passing a list to `np.array()`. You supply every value yourself.
- **Automatically**, using helper functions like `zeros`, `ones`, `full`, `arange` and `linspace`. NumPy generates the values for you.

**Dimensions explained:**

- **1D array** = a single row of numbers (like a list). Example: marks of one student.
- **2D array** = rows and columns (like an Excel sheet or table). Example: marks of many students in many subjects.
- **3D array** = a stack of 2D tables (like multiple Excel sheets). Example: marks of the same class across several years.

A useful way to count dimensions is to count the **levels of square brackets** at the start of the array: `[ ... ]` is 1D, `[[ ... ]]` is 2D, `[[[ ... ]]]` is 3D.

### 3.1 One-Dimensional Array

A 1D array is built from one flat list. It has a single axis (axis 0), so each element needs only one index to be located.

```python
import numpy as np

arr = np.array([10, 20, 30, 40, 50])

print(arr)
```

### 3.2 Two-Dimensional Array

A 2D array is built from a **list of lists**. Each inner list becomes one row, and all rows must have the same length. It has two axes: axis 0 (rows) and axis 1 (columns).

```python
arr = np.array([
    [10, 20, 30],
    [40, 50, 60]
])

print(arr)
```

### 3.3 Three-Dimensional Array

A 3D array is a list of 2D arrays. Think of it as two small tables stacked on top of each other. It has three axes: axis 0 (which table), axis 1 (rows) and axis 2 (columns).

```python
arr = np.array([
    [[1, 2], [3, 4]],
    [[5, 6], [7, 8]]
])

print(arr)
```

### 3.4 Array of Zeros

Useful when you need a blank array that you will fill later, for example as a place to store results inside a calculation. The argument is the number of elements.

```python
arr = np.zeros(5)

print(arr)
```

Output:

```text
[0. 0. 0. 0. 0.]
```

The dots after the zeros show that the values are **decimals** (floats). `np.zeros()` creates `float64` values by default.

### 3.5 Array of Ones

Same idea as zeros, but filled with 1. It is handy as a starting point for multiplication, or for creating a constant array.

```python
arr = np.ones(5)

print(arr)
```

### 3.6 Array with a Specific Value

`np.full(size, value)` fills the array with any value you choose.

```python
arr = np.full(5, 100)

print(arr)
```

Output:

```text
[100 100 100 100 100]
```

### 3.7 Using arange()

`arange()` creates evenly spaced values using a **step size**. It works like Python's `range()`, but returns a NumPy array. The **start** value is included and the **stop** value is **not included**.

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

The general form is `np.arange(start, stop, step)`. If you give only one number, such as `np.arange(5)`, NumPy starts at 0 and gives `[0 1 2 3 4]`.

### 3.8 Using linspace()

`linspace()` creates a **specified number of** evenly spaced values. The difference from `arange()`:

| Function | You decide | End value |
| --- | --- | --- |
| `arange()` | the **step size** | not included |
| `linspace()` | **how many values** you want | **included** |

```python
arr = np.linspace(0, 100, 5)

print(arr)
```

Output:

```text
[  0.  25.  50.  75. 100.]
```

Here NumPy divided the distance from 0 to 100 into 5 equally spaced points, so the gap between neighbours is 25. `linspace()` is widely used when drawing smooth graphs, because you can ask for exactly the number of points you need.

### 3.9 Identity Matrix

An identity matrix has 1s on the diagonal and 0s everywhere else. It is used in matrix mathematics, where it plays the role that the number 1 plays in ordinary multiplication: multiplying any matrix by the identity matrix leaves it unchanged. The argument gives the number of rows and columns.
To check the identity matrix we can use eye() function

```python
arr = np.eye(3)

print(arr)
```

Output:

```text
[[1. 0. 0.]
 [0. 1. 0.]
 [0. 0. 1.]]
```

## 4. NumPy Array Properties

### 4.0 Theory

Every array carries some "information labels" about itself, called **attributes**. They describe the array without making you print all the data. This is very useful when working with large datasets, where you cannot read every number.

An attribute is written **without brackets** (`arr.shape`), unlike a function or method, which has brackets (`arr.flatten()`). You are reading a stored fact about the array, not asking it to do work.

Consider this array for all the examples below:

```python
arr = np.array([
    [10, 20, 30],
    [40, 50, 60]
])
```

### 4.1 Number of Dimensions

`ndim` tells how many "directions" (axes) the array has: 1D, 2D, 3D and so on.

```python
print(arr.ndim)
```

Output: `2`

### 4.2 Array Shape

`shape` gives the size of the array in each direction. It is returned as a **tuple**, written as `(rows, columns)` for a 2D array.

```python
print(arr.shape)
```

Output: `(2, 3)`

It means 2 rows and 3 columns. Shape is the property you will check most often, because many errors in data work come from arrays having unexpected shapes.

### 4.3 Total Number of Elements

`size` counts every value in the array. It equals rows × columns for a 2D array, or the product of all numbers in the shape.

```python
print(arr.size)
```

Output: `6`

### 4.4 Data Type

`dtype` shows the kind of data stored (integer, decimal, etc.). Since every element shares one type, there is only one answer for the whole array.

```python
print(arr.dtype)
```

On most systems this prints `int64`, because the array contains whole numbers.

### 4.5 Memory Size

`itemsize` is the memory occupied by **each element**, measured in **bytes**.

```python
print(arr.itemsize)
```

For `int64` this is 8 bytes, because 64 bits = 8 bytes. Multiplying `itemsize` by `size` gives the total memory used by the data.

| Attribute | What it tells you | Result for the example |
| --- | --- | --- |
| `ndim` | Number of dimensions | 2 |
| `shape` | Size in each dimension | (2, 3) |
| `size` | Total elements | 6 |
| `dtype` | Data type of elements | int64 |
| `itemsize` | Bytes per element | 8 |

---

## 5. NumPy Data Types

### 5.1 Theory

Since every element in an array must be the same type, NumPy needs to know **what type** of data it is storing. The number in a type's name (32, 64) tells how many **bits** of memory each value uses:

- **More bits** = can store bigger numbers or more decimal accuracy, but uses more memory.
- **Fewer bits** = saves memory, but has limits on the size or precision of values.

For most beginner work, NumPy chooses a suitable type automatically (`int64` for whole numbers, `float64` for decimals), so you rarely need to set it yourself. Choosing a smaller type becomes important only when you handle very large datasets and want to save memory.

| Data Type | Description |
| --- | --- |
| int32 | 32-bit integer |
| int64 | 64-bit integer |
| float32 | 32-bit decimal |
| float64 | 64-bit decimal |
| bool\_ | Boolean values |
| complex128 | Complex numbers |

**What do the types mean?**

- **Integer (int):** whole numbers with no decimal part, such as 5 or -20.
- **Float:** numbers with a decimal point, such as 3.14.
- **Boolean (bool\_):** only `True` or `False`.
- **Complex:** numbers with a real and an imaginary part, used mainly in scientific work.

### 5.2 Example: Setting the Type

The `dtype` argument lets you choose the type when creating the array. Here whole numbers are stored as decimals.

```python
arr = np.array([10, 20, 30], dtype=np.float64)

print(arr)
print(arr.dtype)
```

The output shows `[10. 20. 30.]` and `float64`.

### 5.3 Type Conversion

`astype()` changes an array from one type to another. It returns a **new array** and leaves the original unchanged. Converting decimals to integers **cuts off** the decimal part (it does not round).

```python
arr = np.array([10.5, 20.8, 30.2])

new_arr = arr.astype(int)

print(new_arr)
```

Output:

```text
[10 20 30]
```

Notice that 20.8 became 20, not 21. This is called **truncation**. If you want proper rounding, use `np.round()` first.

## 6. NumPy Indexing

### 6.0 Theory

**Indexing** means picking one specific value from an array using its **position number**, just like finding a house using its address.

Two important rules:

1. **Counting starts from 0**, not 1. So the first element is at position `0`, the second at position `1`, and so on. This is called *zero-based indexing* and is used throughout Python.
2. **Negative index counts from the end.** `-1` is the last element, `-2` is the second last, and so on. This is convenient when you want the last value but do not know how long the array is.

For the array `[10, 20, 30, 40, 50]`:

| Value | 10 | 20 | 30 | 40 | 50 |
| --- | --- | --- | --- | --- | --- |
| Positive index | 0 | 1 | 2 | 3 | 4 |
| Negative index | -5 | -4 | -3 | -2 | -1 |

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

Using an index that does not exist (for example `arr[10]` here) raises an `IndexError`.

### 6.1 Two-Dimensional Indexing

In a 2D array, you need **two addresses**: `[row, column]`. The first number selects the row and the second selects the column. Both start from 0.

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

Read `arr[1, 1]` as "row 1, column 1", which is the second row and second column, giving 50.

---

## 7. NumPy Slicing

### 7.1 Theory

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

How to read each line:

- `arr[1:4]` starts at index 1 and stops *before* index 4, so you get indexes 1, 2 and 3.
- `arr[:3]` has no start, so it begins from the first element and stops before index 3.
- `arr[2:]` has no stop, so it runs from index 2 to the end.
- `arr[::2]` takes every second element from the whole array.

### 7.2 Two-Dimensional Slicing

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

The slice `0:2` for rows picks rows 0 and 1, and `0:2` for columns picks columns 0 and 1. The result is the top-left 2×2 block.

**Tip: views and copies.** A slice is a *view* of the original array, not a separate copy. A view shares the same memory, so changing the slice can change the original array. Use `.copy()` if you want an independent copy.

---

## 8. Reshaping Arrays

### 8.1 Theory

**Reshaping** means rearranging the same numbers into a different layout, like taking 12 chocolates from a single row and arranging them into 3 rows of 4. The values and their order stay the same; only the grouping changes.

The only rule: **the total number of elements must stay the same.** 12 elements can become 3×4, 4×3, 2×6 and so on, but not 5×3 (that needs 15), which raises an error.

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

NumPy fills the new shape **row by row**, taking values from the original array in order.

**Shortcut:** Use `-1` to let NumPy calculate one dimension for you. For example, `arr.reshape(3, -1)` automatically becomes 3 rows × 4 columns, because 12 ÷ 3 = 4. Only one dimension can be `-1` at a time.

### 8.2 Flattening

Flattening is the opposite of reshaping into a table: it **converts a multidimensional array into a one-dimensional array**. It reads the values row by row and places them in a single line.

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(arr.flatten())
```

The output is `[1 2 3 4 5 6]`. Flattening is useful when a function expects a simple list of values, or when you want to treat all numbers as one group.

## 9. Arithmetic Operations

### 9.1 Theory

In NumPy, arithmetic works **element by element**. When you add two arrays, the first number is added to the first number, the second to the second, and so on. This is called an **element-wise operation**.

This replaces the need for loops. Instead of writing a loop to add 1000 pairs of numbers, one line `a + b` does it all, and it runs much faster because the looping happens inside NumPy's compiled C code.

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

How to read the results:

- `a + b` → 10+2, 20+4, 30+5 = `[12 24 35]`
- `a - b` → 10-2, 20-4, 30-5 = `[8 16 25]`
- `a * b` → 10×2, 20×4, 30×5 = `[20 80 150]`. This is **not** matrix multiplication; it is element-wise.
- `a / b` → 10÷2, 20÷4, 30÷5 = `[5. 5. 6.]`. Division always gives decimals (floats), which is why the dots appear.
- `a ** 2` → each element raised to the power 2, giving `[100 400 900]`.

### 9.2 Mathematical Functions

NumPy also provides ready-made math functions that apply to every element (these are called **universal functions**, or *ufuncs*).

```python
arr = np.array([1, 4, 9, 16, 25])

print(np.sqrt(arr))
print(np.square(arr))
print(np.power(arr, 2))
print(np.abs([-10, -20, 30]))
```

- `sqrt` → square root of each element
- `square` → each number multiplied by itself
- `power` → raise each element to any power you choose (here, 2)
- `abs` → absolute value (removes the negative sign)

For this array, `np.sqrt(arr)` gives `[1. 2. 3. 4. 5.]` and `np.abs([-10, -20, 30])` gives `[10 20 30]`.

---

## 10. Statistical Operations

### 10.1 Theory

Statistics means **summarizing lots of data using a few meaningful numbers**. Instead of reading 1000 marks, we can say "the average is 78". NumPy has built-in functions for this, which makes it a core tool in data analytics.

**What each measure means:**

| Measure | Simple meaning |
| --- | --- |
| **Sum** | Add everything together |
| **Mean** | The average: sum ÷ count |
| **Median** | The middle value after sorting. Not affected much by extreme values |
| **Min / Max** | Smallest / largest value |
| **Variance** | How spread out the numbers are from the average (in squared units) |
| **Standard deviation** | Spread of data in the same units as the data. Small = values are close to average; large = values are scattered |
| **Percentile** | The value below which a given percentage of data falls. 75th percentile = 75% of values are below it |

**Mean vs Median:** If salaries are 20k, 22k, 25k and 500k, the mean is pulled up by the big value, while the median stays closer to a "typical" salary. This is why analysts often check both: a large gap between mean and median is a sign of extreme values (outliers) in the data.

**Variance and standard deviation:** Variance is found by taking how far each value is from the mean, squaring those distances, and averaging them. Because the distances are squared, the units are squared too (marks²). The standard deviation is the square root of the variance, which brings the answer back to the original units (marks), so it is easier to interpret.

Consider student marks:

```python
marks = np.array([70, 80, 90, 60, 85, 95])
```

### 10.2 Sum

```python
print(np.sum(marks))
```

The result is `480`.

### 10.3 Mean

```python
print(np.mean(marks))
```

The result is `80.0`, because 480 ÷ 6 = 80.

### 10.4 Median

First sort the values (60, 70, 80, 85, 90, 95). With an even number of values, the median is the average of the two middle ones.

```python
print(np.median(marks))
```

The result is `82.5`, which is the average of 80 and 85.

### 10.5 Minimum

```python
print(np.min(marks))
```

The result is `60`.

### 10.6 Maximum

```python
print(np.max(marks))
```

The result is `95`.

### 10.7 Standard Deviation

```python
print(np.std(marks))
```

### 10.8 Variance

```python
print(np.var(marks))
```

By default NumPy calculates the **population** standard deviation and variance (dividing by n). For a *sample*, pass `ddof=1`, as in `np.std(marks, ddof=1)`.

### 10.9 Percentile

```python
print(np.percentile(marks, 75))
```

This gives the value below which 75% of the marks fall.

### 10.10 Sorting

```python
print(np.sort(marks))
```

The output is `[60 70 80 85 90 95]`. `np.sort()` returns a sorted **copy**; the original array is not changed.

### 10.11 The `axis` parameter (important for 2D data)

In a 2D array, you can choose the direction of calculation:

- `axis=0` → calculate **down the columns** (one result per column).
- `axis=1` → calculate **across the rows** (one result per row).

A simple way to remember: the `axis` you give is the one that gets *collapsed*. With `axis=0` the rows collapse into one, leaving one value per column. With `axis=1` the columns collapse, leaving one value per row.

```python
data = np.array([
    [85, 78, 90],
    [70, 65, 75]
])

print(np.mean(data, axis=0))
print(np.mean(data, axis=1))
```

The first line gives column averages `[77.5 71.5 82.5]`; the second gives row averages `[84.33... 70.]`.

---

## 11. Broadcasting

### 11.1 Theory

Normally, to add two arrays they must be the same size. **Broadcasting** is NumPy's smart feature that **automatically stretches the smaller array** so the operation can still happen. You do not need to copy or repeat data yourself. The stretching is conceptual: NumPy does not actually make extra copies in memory, which keeps it fast.

Two common situations:

1. **Scalar with array:** a single number is applied to every element.
2. **Small array with big array:** the small array is repeated across the rows (or columns) of the bigger one.

**Rule of thumb:** Compare shapes from the right side. Two dimensions are compatible if they are **equal**, or **one of them is 1** (or missing). If neither condition holds, NumPy raises an error.

### 11.2 Example 1: Scalar Broadcasting

```python
arr = np.array([10, 20, 30])

print(arr + 5)
```

Output:

```text
[15 25 35]
```

The single number 5 is treated as if it were `[5, 5, 5]`.

### 11.3 Example 2: Array Broadcasting

Here `b` (shape 3) is stretched across both rows of `a` (shape 2×3). Comparing shapes from the right: 3 and 3 are equal, and the missing dimension of `b` is treated as 1, so they are compatible.

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

## 12. Filtering and Conditional Operations

### 12.1 Theory

**Filtering** means keeping only the data that meets a condition, like selecting only students who scored 40 or more.

It works in two steps:

1. NumPy applies the condition to every element and produces an array of **True / False** values, called a *boolean mask*.
2. When you put that mask inside the square brackets, NumPy keeps only the elements marked **True**.

For multiple conditions, use:

| Operator | Meaning | Rule |
| --- | --- | --- |
| `&` | AND | both conditions must be true |
| `\|` | OR | at least one condition must be true |
| `~` | NOT | reverses True and False |

**Important:** Always put each condition inside **brackets ( )** when combining them. Do not use Python's `and` / `or` with arrays; they will cause an error, because Python cannot decide whether a whole array is "True" or "False".

```python
marks = np.array([45, 60, 75, 30, 90, 85])

passed = marks[marks >= 40]

print(passed)
```

Output:

```text
[45 60 75 90 85]
```

Behind the scenes, `marks >= 40` produces the mask `[True True True False True True]`. Only the positions marked `True` are kept, so 30 is removed.

### 12.2 Multiple Conditions

This keeps marks that are at least 50 **and** at most 80.

```python
marks = np.array([45, 60, 75, 30, 90, 85])

result = marks[(marks >= 50) & (marks <= 80)]

print(result)
```

The output is `[60 75]`.

### 12.3 Using np.where()

`np.where(condition, value_if_true, value_if_false)` works like an **if-else for the whole array**. It does not remove anything; it **replaces** values based on the condition, so the result has the same length as the input.

```python
marks = np.array([35, 80, 45, 90, 25])

result = np.where(marks >= 40, "Pass", "Fail")

print(result)
```

The output is `['Fail' 'Pass' 'Pass' 'Pass' 'Fail']`.

**Filtering vs `where`:** use filtering (`marks[mask]`) when you want to *shorten* the data to matching items. Use `np.where` when you want to *label or transform* every item.

### 12.4 Counting Conditions

Since `True` counts as 1 and `False` as 0, we can count how many values meet a condition.

```python
print(np.count_nonzero(marks >= 40))
```

For the marks above, this prints `3` (the marks 80, 45 and 90).

---

## 13. Joining and Splitting Arrays

### 13.1 Theory

Sometimes data comes in pieces and needs to be combined, or one big array needs to be divided into parts.

- **Joining** = attaching arrays together, like connecting train coaches.
- **Splitting** = cutting one array into smaller arrays.

**Which join to use?**

| Function | What it does |
| --- | --- |
| `concatenate` | Joins arrays end to end along an existing direction |
| `vstack` | Stacks arrays **vertically** (one below another, adding rows) |
| `hstack` | Stacks arrays **horizontally** (side by side, adding columns) |

### 13.2 Concatenate

Note that the arrays are passed together inside one **tuple** (the extra brackets).

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

result = np.concatenate((a, b))

print(result)
```

The output is `[1 2 3 4 5 6]`.

### 13.3 Vertical Stack

`vstack` places the second array *below* the first, creating a 2D array with two rows.

```python
a = np.array([1, 2])
b = np.array([3, 4])

print(np.vstack((a, b)))
```

Output:

```text
[[1 2]
 [3 4]]
```

### 13.4 Horizontal Stack

`hstack` places the second array *beside* the first, giving one longer row.

```python
print(np.hstack((a, b)))
```

The output is `[1 2 3 4]`.

### 13.5 Splitting

`np.split(arr, 3)` divides the array into **3 equal parts**. The array length must be divisible by the number of parts, otherwise NumPy gives an error (use `np.array_split()` for unequal parts).

```python
arr = np.array([10, 20, 30, 40, 50, 60])

result = np.split(arr, 3)

print(result)
```

The result is a **list of arrays**: `[array([10, 20]), array([30, 40]), array([50, 60])]`.

---

## 14. Random Numbers

### 14.1 Theory

Random numbers are used to **create sample data, simulate situations, and shuffle or pick samples**. When you are learning, you do not always have a real dataset, so random numbers help you practice.

Computers do not produce truly random numbers; they follow a mathematical formula that *looks* random. This is called **pseudo-random**. Because it is formula-based, we can control it using a **seed**.

**Seed:** A starting number for the formula. Using the same seed gives the **same random numbers every time**, which is important when you want your results to be repeatable (for example, when sharing your work or testing).

**Main functions:**

- `randint(low, high)` → random whole numbers (the high value is not included).
- `rand()` → random decimals between 0 and 1, evenly spread.
- `randn()` → random decimals from the **normal distribution** (bell curve), centered around 0. Values can be negative, and most fall close to 0.

### 14.2 Examples

```python
# Random integer
print(np.random.randint(1, 100))

# Random decimal
print(np.random.rand(5))

# Random normal distribution
print(np.random.randn(5))
```

The output changes every time you run the code, because no seed has been set.

### 14.3 Reproducible Random Data

```python
np.random.seed(42)

print(np.random.randint(1, 100, 5))
```

Because the seed is fixed at 42, running this again gives the same five numbers each time.

For new code, the recommended approach uses the newer **Generator** interface:

```python
rng = np.random.default_rng(42)

print(rng.integers(1, 100, size=5))
```

`default_rng(42)` creates a random number generator with its own seed, and `rng.integers()` is the modern counterpart of `randint`. It is preferred because the generator is a self-contained object, which makes results easier to control in larger programs.

## 15. File Handling with NumPy

### 15.0 Theory

Real-world data lives in **files**, not typed inside code. File handling means **saving** your arrays so you can use them later, and **loading** data from files into arrays.

NumPy supports two kinds of files:

| Kind | Extension | Advantages | Drawbacks |
| --- | --- | --- | --- |
| **Binary** | `.npy` | NumPy's own format; fast and exact (keeps shape and data type) | Cannot be read in Notepad |
| **Text** | `.txt`, `.csv` | Human-readable; can be opened in Excel or Notepad | Slightly slower; less exact |

### 15.1 Saving an Array

`np.save()` writes the array to a binary `.npy` file.

```python
arr = np.array([10, 20, 30, 40, 50])

np.save("marks.npy", arr)
```

### 15.2 Loading an Array

`np.load()` reads the `.npy` file back into an array, with the same shape and data type as when it was saved.

```python
data = np.load("marks.npy")

print(data)
```

### 15.3 Saving as Text File

`np.savetxt()` writes the values in readable text form, so you can open the file in any text editor.

```python
arr = np.array([10, 20, 30, 40, 50])

np.savetxt("marks.txt", arr)
```

### 15.4 Loading Text File

```python
data = np.loadtxt("marks.txt")

print(data)
```

Values loaded from a text file come back as decimals (floats) by default.

### 15.5 Working with CSV Files

**CSV** stands for *Comma-Separated Values*: a simple text file where each line is a row and commas separate the columns. It is one of the most common formats for sharing data.

Create a file named `students.csv`:

```csv
Name,Python,SQL,Statistics
Amit,85,78,90
Rahul,70,65,75
Priya,95,88,92
Neha,60,72,68
```

Read numerical columns using NumPy. The three extra arguments matter:

- `delimiter=","` → tells NumPy that commas separate the values.
- `skiprows=1` → skips the header line (column names).
- `usecols=(1, 2, 3)` → reads only the number columns and ignores the Name column (since text would cause an error). Column numbering starts at 0.

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

## 16. NumPy with Pandas

### 16.1 Theory

**Pandas** is a library for working with **tables of data**, like Excel sheets inside Python. Its main structure is the **DataFrame**: a table with rows, columns and column names. It can hold mixed data (text, numbers, dates).

How the two libraries differ and cooperate:

- **NumPy** = fast math on pure numbers.
- **Pandas** = organizing, labeling, cleaning and reading data tables.

In practice, Pandas stores its numeric data using NumPy underneath. You can pull the numbers out as a NumPy array (`to_numpy()`), do calculations, and put the results back as a new column.

### 16.2 Installation

```bash
pip install pandas
```

### 16.3 Importing

```python
import numpy as np
import pandas as pd
```

`pd` is the standard alias for Pandas, just as `np` is for NumPy.

### 16.4 Example: Student Performance

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

### 16.5 Convert Pandas Columns into NumPy Arrays

Selecting one column with `df["Python"]` gives a Pandas Series. `to_numpy()` converts it into a plain NumPy array so you can use NumPy functions on it.

```python
python_marks = df["Python"].to_numpy()

print(python_marks)
```

### 16.6 Calculate Average Using NumPy

Selecting several columns (using a list of names inside double brackets) gives a table of numbers; `axis=1` calculates the average across each student's row. The result is stored as a new column called `Average`.

```python
marks = df[["Python", "SQL", "Statistics"]].to_numpy()

df["Average"] = np.mean(marks, axis=1)

print(df)
```

### 16.7 Calculate Highest Marks

```python
df["Highest"] = np.max(marks, axis=1)

print(df)
```

### 16.8 Find Students Who Passed

Here `np.where()` creates a new `Result` column that says Pass or Fail for every student.

```python
df["Result"] = np.where(df["Average"] >= 40, "Pass", "Fail")

print(df)
```

### 16.9 Find Topper

`idxmax()` returns the row position of the highest value, and `loc` fetches that whole row.

```python
topper = df.loc[df["Average"].idxmax()]

print(topper)
```

### 16.10 Export Result

```python
df.to_csv("student_results.csv", index=False)
```

`index=False` prevents Pandas from saving the extra row-number column.

---

## 17. NumPy with Matplotlib

### 17.1 Theory

Numbers in tables are hard to understand quickly. A **chart** shows patterns instantly. **Matplotlib** is Python's most popular library for drawing charts and graphs.

NumPy prepares and calculates the numbers, and Matplotlib draws them.

**Choosing the right chart:**

| Chart | Best used for |
| --- | --- |
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

### 17.2 Installation

```bash
pip install matplotlib
```

### 17.3 Importing

```python
import numpy as np
import matplotlib.pyplot as plt
```

`plt` is the standard alias for Matplotlib's `pyplot` module.

### 17.4 Line Chart

Points are connected by a line to show how something changes, such as sales across months. `marker="o"` draws a dot at each data point.

```python
months = np.array(["Jan", "Feb", "Mar", "Apr", "May"])

sales = np.array([10000, 15000, 12000, 18000, 25000])

plt.plot(months, sales, marker="o")

plt.title("Monthly Sales")
plt.xlabel("Months")
plt.ylabel("Sales")

plt.show()
```

### 17.5 Bar Chart

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

### 17.6 Pie Chart

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

### 17.7 Histogram

Groups values into ranges called **bins** and shows how many values fall in each bin. Unlike a bar chart, it is used for **continuous numeric data**. Here `bins=5` splits the marks into 5 ranges, and `edgecolor` draws an outline around each bar so they are easy to tell apart.

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

### 17.8 Scatter Plot

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

### 17.9 Multiple Lines

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

## 18. Mini Project: Student Performance Analysis

### 18.1 Objective

Analyze student marks using NumPy, Pandas and Matplotlib.

### 18.2 Theory

This project follows the **real workflow of a data analyst**:

1. **Collect** data (create the dataset).
2. **Calculate** new useful numbers (total, average).
3. **Categorize** (assign grades).
4. **Find insights** (topper, subject averages).
5. **Visualize** (charts).
6. **Share** (save results to a file).

Each library does what it is best at: Pandas holds the table, NumPy calculates, and Matplotlib draws. Notice how every step builds on the one before it. This pattern of collect, calculate, categorize, analyze, visualize and share appears in almost every analytics task, whatever the dataset.

### Step 1: Import Libraries

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

### Step 2: Create Dataset

The data is stored in a dictionary and converted into a DataFrame. In real projects you would usually load it from a CSV file instead.

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

Total = sum of all subjects for each student. Average = total ÷ number of subjects. We convert the three subject columns into a NumPy array and use `axis=1` so each calculation runs across one student's row.

```python
subjects = ["Python", "SQL", "Statistics"]

marks = df[subjects].to_numpy()

df["Total"] = np.sum(marks, axis=1)

df["Average"] = np.mean(marks, axis=1)

print(df)
```

### Step 4: Assign Grades

`np.select()` is like a multi-level if-elif-else. It checks the conditions in order and gives the grade of the first one that is true. Anything that matches none gets the `default` grade. Because the order matters, the conditions go from the highest cut-off to the lowest.

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

| Average | Grade |
| --- | --- |
| 90 and above | A+ |
| 80 to below 90 | A |
| 70 to below 80 | B |
| 60 to below 70 | C |
| 40 to below 60 | D |
| below 40 | F |

### Step 5: Find Topper

The topper is the student with the highest total marks.

```python
topper = df.loc[df["Total"].idxmax()]

print("Class Topper:")
print(topper)
```

### Step 6: Calculate Subject Averages

This shows which subject the class is strongest or weakest in. `axis=0` calculates down each column, giving one average per subject.

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

## 19. Practice Questions

### 19.1 Theory

Reading is not enough to learn programming; **you learn by doing**. Try each question yourself first, then check the notes if you get stuck. The questions are arranged from easy to hard so your confidence builds step by step. Making mistakes and reading the error messages is a normal and valuable part of learning.

### Beginner Level

1. Create a NumPy array containing numbers from 1 to 20.
2. Create an array of 10 zeros.
3. Create an array of 10 ones.
4. Find the maximum and minimum values.
5. Calculate the mean and median.
6. Extract the first five elements from an array.
7. Reverse an array.
8. Convert a one-dimensional array into a 3x3 matrix.

### Intermediate Level

1. Create an array of 20 random integers.
2. Find all values greater than 50.
3. Count the number of even numbers.
4. Replace values below 40 with zero.
5. Calculate row-wise and column-wise averages.
6. Combine two arrays using concatenate().
7. Split an array into four equal parts.
8. Calculate standard deviation and variance.

### Advanced Level

1. Create a 5x5 random matrix.
2. Find the maximum value in every row.
3. Normalize an array using min-max normalization. *(Hint: new value = (x − min) ÷ (max − min), which scales all values between 0 and 1.)*
4. Calculate the correlation between two numerical arrays. *(Hint: correlation tells how strongly two variables move together. Try `np.corrcoef()`.)*
5. Generate a dataset and identify outliers using the IQR method. *(Hint: IQR = Q3 − Q1. Values below Q1 − 1.5×IQR or above Q3 + 1.5×IQR are outliers, meaning unusually small or large values.)*
6. Load a CSV file and perform statistical analysis.
7. Combine NumPy, Pandas and Matplotlib to analyze a dataset.

---

## 20. Important NumPy Functions Cheat Sheet

### 20.1 Theory

A cheat sheet is a **quick-revision table**. You do not need to memorize everything; just remember what each function is *for*, and you can look up the exact usage when needed.

| Function | Purpose |
| --- | --- |
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

## Conclusion

NumPy is an essential library in the Data Analytics ecosystem. It provides efficient numerical calculations and works closely with:

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
