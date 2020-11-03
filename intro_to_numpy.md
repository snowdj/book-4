# Intro to numpy
---


**Overview.** We will learn about the key scientific computing packages in python: **`numpy`**.

**Pythons.**  NdArray

**Trigger warning.**  Technical content, cannot be mastered without effort.

---

What is numpy, a short for **Numerical Python**. It can be used for high performance computing and data analysis. In our case, we will just use some basic elements of numpy, but its worth knowing about because of its power and that it backs other packages we will use later. There are essentially three core features.

* **Scientific Computation**: It provides core numerical operations like ``exp``,``log``, random number generators and more!

* **Efficiency**: it provides the most efficient data structure in python: `ndarray` for this type of computing. Imagine when you need to conduct calculations on more than 200k rows with 10k columns over and over again.

* **Data analysis**: though itself does not provide very high-level data analytical function as `pandas`, having an understanding of it will help us use tools in pandas with less pain.


This note book will focus on the key data structure in `numpy` and their attributes and methods. And then we will perform basic scientific computations in `numpy`.

## Importing the package

How do import the package? We know this. We type:

```python
import numpy as np
```

This says import the package `numpy` then the "as np" says call it `np` (our alias)
this just simplifies our life without having to always type `numpy`, we just
type `np`. IF you're lost on this, go back to our chapter on [importing packages](https://nyudatabootcamp.gitbooks.io/data-bootcamp/content/packages.html).

Now that we have this done, let's first get to know the most important data structure in `numpy`.

### Array

The `ndarray` is the primary building block of numpy. It enables us to perform mathematical computations efficiently using similar syntax to the equivalent operations for scalar elements as we learned in python fundamental notebook 1.

So let's create an array object via `array` methods in `numpy`.

```python
In [2]: data1 = [3.4,2,7,1,5]

In [3]: arr1 = np.array(data1)

In [4]: arr1
Out[4]: array([3.4, 2. , 7. , 1. ])
```
Let's create an another array

```python
In [5]: data2 = [5,2,1,3,4]

In [6]: arr2 = np.array(data2)
```
Now we can do some simple computations like we've done for scalars in python fundamental notebook 1.

```python
In [7]: arr1+arr2
Out[7]: array([8.4, 4. , 8. , 4. , 9. ])
```

```python
In [8]: arr1*arr2
Out[8]: array([17.,  4.,  7.,  3., 20.])
```

Here is another example of an array. This one is composed of two lists of the same length.

```python
In [9]: arr4=np.array([[2,3,4],[8,5,7]])

In [10]: arr4
Out[10]:
array([[2, 3, 4],
       [8, 5, 7]])
```
Notice what this is doing. It is effectively creating a 2 by 3 array. That is there are two rows and three columns (note how this is looking like a table or a data set). So what is happening here is that the individual list is defining a row, then however many elements within each row are the number of columns.

### Array Methods

Let's use one of the built in methods associated with an ``ndarray`` to explore this.  One is its `.shape`. This will be reported as the number of rows and columns if its a two dimensional array. What should we expect?

```python
In [11]: arr4.shape
Out[11]: (2, 3)
```
So it tells us that the array is of shape two rows and three columns. **mtwn** but this is standard matrix convention, rows first then columns. We can also use built-in methods to initialize 1-d or 2-d arrays:

```python
In [12]: arrZeros = np.zeros((2,3))

In [13]: arrZeros
Out[13]:
array([[0., 0., 0.],
       [0., 0., 0.]])
```
So this is creating an array which is of shape two rows and three columns (again rows first, columns second). Below we can create an array full of ones.

```python
In [14]: arrOnes = np.ones((2,2))

In [15]: arrOnes
Out[15]:
array([[1., 1.],
       [1., 1.]])
```
Here is an interesting one, it has one on only the diagonal and zeros elsewhere. This is called an identity matrix.

```python
In [16]: arrEyes = np.eye(3)

In [17]: arrEyes
Out[17]:
array([[1., 0., 0.],
       [0., 1., 0.],
       [0., 0., 1.]])
```
So what it did was create a square matrix with three rows and three columns, then the ones down the diagonal.


In fundamental notebook 2, we have learned the `range` object when using it with for loops. Here we present the `numpy` array version of it.
```python
np.arange(0,10,2)
```

### Transpose an array

In `numpy`, transpose an 1-d or 2-d array is super easy and fast via `.T`.

```python
print(arrZeros.shape)

print(arrZeros.T.shape)
```

### A gentle introduction to broadcasting

Arrays with different sizes cannot be added, subtracted, or generally be used in arithmetic. A way to overcome this is to duplicate the smaller array so that it is the dimensionality and size as the larger array. This is called array **broadcasting**. It is available in `numpy` when performing array arithmetic, which can greatly speed up and simplify your code.

Here is an example:

```python
arr3 = arr1+2
arr3
```
First, note that 2 is a scalar and its being added to the array which is of dimension 5 by 1. When they are added together, it broadcasts the scalar value **2** five times and add it to the each value in the **arr1**. So rather than having to first create an array full of 2s, numpy does it for us.

---
### Time to practice

**Exercises.** Initialize a 4 by 1 array with 2 and named it as arrE1.

**Exercises.** Initialize a 1 by 4 array with number 3 and named it as arrE2.

**Exercises.** Can you perform an element wise add operation of the arrE1 and arrE2?

**Exercises (challenging).** How to create a 3 by 3 array with only zeros in diagonal while the rest is 2?

---
## Slicing

Slicing in `numpy` array is like we have done for lists. Let's first define a two-dimensional array and then review what we have learned.



```python
arr4=np.array([[2,3,4],[8,5,7]])
arr4
---

array([[2, 3, 4], [8, 5, 7]])
```

How to get number **3** from the above 2-dimensional arrays? Try these three different ways:


```python
arr4[0,1]
---
    3
```

```python
arr4[0][1]
---
    3
```

```python
arr4[0,1:2]
```




    array([3])



Can you figure out why this line of code only return one number instead of 3 and 4?  Be careful with the indexing hassles for different data structure, it may result potential errors and hard to identify. In addition, we can continue using **forward** counter, a **backward** counter, and **:** operator like we did with list or string data structures when selecting data.

---
## Numerical Methods


### Elementwise Methods

Remember in python fundamental notebook 1, when we want to compute the log of a scalar, it returns an error, saying not defined. Yes, it is. Since in python, the majority of math operations like log, exp and so on are defined in `numpy` package.

Let's see the following examples...


```python
arr1_log = np.log(arr1)
arr1_log
```


```python
arr1_exp = np.exp(arr1)
arr1_exp
```


```python
arr1_sqrt = np.sqrt(arr1)
arr1_sqrt
```

### Array-wise Operation


```python
arr4
```




    array([[2, 3, 4],
           [8, 5, 7]])



What will we get in the following？


```python
np.sum(arr4)
```




    29



Interesting, it only returns one number which is the sum of all the elements of the array.

But can we perform row or column sum?

Yes, we can...


```python
np.sum(arr4,axis=0) # Column Sum
```




    array([10,  8, 11])




```python
np.sum(arr4,axis=1) # Row Sum
```




    array([ 9, 20])



I know what does **axis** mean in the above function call may seem confusing right now. Let's remember one principle: when setting axis, always think about the operation first, whether it will be done across column or across row. If the former, setting axis = 1, otherwise, sett

And we'll see more examples about this in next "intro to pandas" notebook.

---
### Time to practice

**Exercises.** How to compute the **column** mean?

**Exercises.** How to compute the **column** mean in second and third column?

**Exercises.** How to compute the **row** mean?

### Random number generator

We can use a random number generator to generate an `numpy` with samples from a  “standard normal” distribution in specified shape.

For example, we generate a 2 by 4 random number array...


```python
np.random.randn(2,4)
```

---
## Summary

**Congratulations!** First, it's amazing that you have made it this far. Reflect on what you knew before working through this notebook, namely what we did in python fundamental notebooks. Now reflect on what you can do...AMAZING!!! Let us summarize some key things that we covered.

* **Numpy Core Objects**: An `array` with one demension is essentially just a vector of data while a `array` with two dimension can be thought a table of data with rows and columns. We will not cover dimension more than 2 in this course.

* **Understanding the 2-d `Array`**:
    * Learn how to initialize an array with desired values and dimensions.
    * Become familiar with python built-in computations, e.g., `+`, `-`, among 1-d or 2-d arrays and the implicit usage of broadcasting in them.
    * Know how to grab elements from an arraym, the elements could be a number or part of the original arrays.
    * Two types of useful mathmatic methods in array.
        * Operations perform on each individual elements of the array, e.g., `np.log`.
        * Operations across columns or rows, e.g., `np.sum`. This one require the correctly setting the `axis` parameters in the `numpy` methods.

* **Axis Understanding**: when setting **axis**, always think about the operation first, whether it will be done across column or across row. If the former, setting axis = 1. For this course, the **axis** will always be **0** or **1**. We will cover more examples in "intro to pandas notebook".
