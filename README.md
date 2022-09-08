# Computational Complexity

## Introduction to Algorithms

*(Thomas H. Cormen, Charles E. Leiserson, Ronald L. Rivest, and Clifford Stein. 2009. Introduction to Algorithms, Third Edition (3rd. ed.). The MIT Press.)*

Informally, an ***algorithm*** is any well-defined computational procedure that
takes some value, or set of values, as ***input*** and produces some value, or set
of values, as ***output***.  An algorithm is thus a sequence of computational
steps that transform the input into the output.

We can also view an algorithm as a tool for solving a well-specified
***computational problem***. The statement of the problem specifies in general
terms the desired input/output relationship. The algorithm describes a specific
computational procedure for achieving that input/output relationship.

### Example: Sorting Problem

 * **Input:** A sequence of $n$ numbers $a_1$, $a_2$, ... $a_n$.
 * **Output:** A permutation (reordering) $b_1$, $b_2$, ... $b_n$ of the initial
   sequence such that $b_1 \leq b_2 \leq ... \leq b_n$.

## Algorithm Efficiency

*(Prof. Erik Demaine, Dr. Jason Ku, Prof. Justin Solomon, 2020. Lecture Notes. 6.006 Introduction To Algorithms)*

What makes a computer program efficient? One program is said to be more
***efficient*** than another if it can solve the same problem input using fewer
resources. We expect that a larger input might take more time to solve than
another input having smaller size. In addition, the resources used by a program,
e.g. storage space or running time, will depend on both the algorithm used and
the machine on which the algorithm is implemented. We expect that an algorithm
implemented on a fast machine will run faster than the same algorithm on a
slower machine, even for the same input. We would like to be able to compare
algorithms, without having to worry about how fast our machine is. So in this class, we compare algorithms based on their ***asymptotic performance*** relative to
problem input size, in order to ignore constant factor differences in hardware performance.

## Running Time Analysis

Assume `n = A.length`.

<textarea rows="12" cols="80">
InsertionSort(A)                   // Cost  Times
1. for j = 1; j < A.length; j++  // c_1   ?
2.   key = A[j]                  // c_2   ?
3.   // Insert A[j] into
     // the sorted sequence
     // A[1..j-1].
4.   i = j - 1                   // c_4   ?
5.   while i >= 0 and A[i] > key // c_5   ?
6.     A[i + 1] = A[i]           // c_6   ?
7.     i = i - 1                 // c_7   ?
8.   A[i + 1] = key              // c_8   ?
</textarea>

For each $j = 1,2,...n-1$, let $t_j$ denote the number of times the **while** loop test in line 5 is executed for that value of $j$.

<details>
<summary>Answer</summary>

```pascal
InsertionSort(A)                  // Cost  Times
1. for j = 1; j < A.length; j++  // c_1   n
2.   key = A[j]                  // c_2   n - 1
3.   // Insert A[j] into
     // the sorted sequence
     // A[0..j-1].
4.   i = j - 1                    // c_4   n - 1
5.   while i >= 0 and A[i] > key  // c_5   sum(t_j for j=1..n-1)
6.     A[i + 1] = A[i]            // c_6   sum(t_j - 1 for j=1..n-1)
7.     i = i - 1                  // c_7   sum(t_j - 1 for j=1..n-1)
8.   A[i + 1] = key               // c_8   n-1
```
</details>
</br>

Let $T(n)$ be the running time of the insertion sort on an input of $n$ values. Then

$$T(n) = c_1n +c_2(n-1) + c_4(n-1) + c_5\sum_{j=1}^{n-1} t_j + c_6\sum_{j=1}^{n-1}(t_j-1) + c_7\sum_{j=1}^{n-1}(t_j - 1) + c_8(n-1)$$

### Best Case Analysis

<hr/>
<details>
<summary>When the best case for the insertion sort occurs?</summary>

The best case for the insertion sort occurs if they array is already sorted.
</details>
<hr/>
