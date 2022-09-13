# Computational Complexity

## References
Thomas H. Cormen, Charles E. Leiserson, Ronald L. Rivest, and Clifford Stein.
2009. Introduction to Algorithms, Third Edition (3rd. ed.). The MIT Press.

Prof. Erik Demaine, Dr. Jason Ku, Prof. Justin Solomon, 2020. Lecture Notes.
6.006 Introduction To Algorithms.

## Introduction to Algorithms

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

### Excercise: Insertion Sort Algorithm

Review the [following](https://go.dev/play/p/6DeRwqagVT7) algorithm. Calculate how many times each line is executed.

* Assume $n =$ `A.length`.
* For each $j = 1,2,...n-1$, let $t_j$ denote the number of times the **while** loop test in line 6 is executed for that value of $j$.

<details>
<summary>Answer</summary>

```pascal
1. InsertionSort(A)                                       // Cost  Times
2.   for j = 1; j < A.length; j++                         // c_1   n
3.     key = A[j]                                         // c_2   n - 1
4.     // Insert A[j] into the sorted sequence A[1..j-1].
5.     i = j - 1                                          // c_3   n - 1
6.     while i >= 0 and A[i] > key                        // c_4   sum(t_j for j=1..n-1)
7.       A[i + 1] = A[i]                                  // c_5   sum(t_j - 1 for j=1..n-1)
8.       i = i - 1                                        // c_6   sum(t_j - 1 for j=1..n-1)
9.     A[i + 1] = key                                     // c_7   n - 1
```
</details>
</br>

Let $T(n)$ be the running time of the insertion sort on an input of $n$ values. Then

$$T(n) = c_1n +c_2(n-1) + c_3(n-1) + c_4\sum_{j=1}^{n-1} t_j + c_5\sum_{j=1}^{n-1}(t_j-1) + c_6\sum_{j=1}^{n-1}(t_j - 1) + c_7(n-1).$$

<hr/>

<details>
<summary>When the best case for the insertion sort occurs?</summary>

The best case for the insertion sort occurs if they array is already sorted. For each $j = 1, 2, ..., n-1$, $A[i] \leq key$ in line 6 when $i$ has its initial value of $j - 1$. Thus $t_j = 1$ for $j = 1, 2, ..., n-1$, and the best-case running time is

$$T(n) = c_1n + c_2(n-1) +c_3(n-1) + c_4(n-1) + c_7(n-1).$$

$$T(n) = (c_1 + c_2 + c_3 + c_4 + c_7)n - (c_2 - c_3 - c_4 - c_7).$$

We can express this running tiume as $an + b$ for *constants* $a$ and $b$ that depend on the statment costs $c_i$; it is thus a **linear function** of $n$.

</details>
<hr/>

<details>
<summary>When the worst case for the insertion sort occurs?</summary>

The worst case for the insertion sort occurs if the array is in reverse sorted order (in decreasing order). We must compare each element $A[j]$ with each element in the entire sorted subarray $A[1..j-1]$, and so $t_j = j+1$ for $j=1,2,...,n-1$.
Note that

$$\sum_{j=1}^{n-1}(j+1) = \frac{n-1}{2}(1 + n) = \frac{n(n+1)}{2} - 1$$

and 

$$\sum_{j=1}^{n-1}(j + 1 - 1) = \sum_{j=1}^{n-1}j = \frac{n-1}{2}(1 + n - 1) = \frac{n(n - 1)}{2}.$$

$$T(n) = c_1n + c_2(n-1) + c_3(n-1) + c_4\left(\frac{n(n+1)}{2} - 1\right) + c_5\left(\frac{n(n - 1)}{2}\right) + c_6\left(\frac{n(n - 1)}{2}\right) + c_7(n-1).$$

$$T(n) = \left(\frac{c_4}{2} + \frac{c_5}{2} + \frac{c_6}{2}\right)n^2 + \left(c_1 + c_2 + c_3 + \frac{c_4}{2} - \frac{c_5}{2} - \frac{c_6}{2} + c_7\right)n - \left(c_2 + c_3 + c_4 + c_7\right).$$

We can express this worst-case running time as $an^2 + bn + c$ for constants $a$, $b$, and $c$ that again depend on the statements cost $c_i$; it is thus a **quadratic function** of $n$.

</details>

<hr/>

We usually concentrate on finding only the **worst-case running time**, that is, the longest running time for *any* input of size *n*. The worst-case running time of an algorithm gives us an upper bound on the running time for any input. Knowing it provides a guarantee that the algorithm will never take any longer.

Assumptions we already made:

* Every statement has a fixed cost.
* Ignored the abstract costs $c_i$.

Further assumptions:

* It is **order of growth** of the running time that really interests us. We consider only the leading term of a formula, e.g. $an^2$, since the lower-order terms are relatively insignificant for large values of $n$.
* We also ignore the leading's term constant coefficient, since constant factors are less significant that the rate of growth in determining computational efficiency for large inputs.

We write that **the insertion sort has the worst-case running time (time complexity) of $O(n^2)$**.

For large enough inputs, a $O(n^2)$ algorithm, for example, will run more quickly in the worst case than a $O(n^3)$ algorithm.

Express the function $n^3 - 100n^2 - 100n + 3$ in terms of $O$-notation.

<details>
<summary>Answer</summary>

$$n^3 - 100n^2 - 100n + 3 = O(n^3)$$

</details>

## Comparing time complexities

![](https://miro.medium.com/max/700/1*FkQzWqqIMlAHZ_xNrEPKeA.png)

## Rules

1. Different steps get added:

   ```go
   func something() {
     doStep1() // O(a)
     doStep2() // O(b)
   } // O(a + b)
   ```

2. Drop constants:

   ```go
   func minMax1(arr []int) (min int, max int) {
    for _, el := range arr {
      min = math.Min(el, min)
    } // O(n)
    for _, el := range arr {
      max = math.Max(el, max)
    } // O(n)
   } // O(2n) = O(n)

   func minMax2(arr []int) (min int, max int) {
     for _, el := range arr {
       min = math.Min(el, min)
       max = math.Max(el, max)
     } // O(n)
   } // O(n)
   ```

3. Different inputs -> different variables

   ```go
   func intersectionSize(a, b []int) int {
     count := 0
     for _, el1 := range a {
       for _, el2 := range b {
         if el1 == el2 {
           count++
         }
       }
     }
     return count
   } // O(mn), where m is the size of m, and n is the size of b.
   ```

4. Drop non-dominant terms

   ```go
   func f(arr []int) {
     max := 0
     for _, el := arr {
       max = math.Max(el, max)
     } // O(n)
     fmt.Println(max)
     for _, el := arr {
       for _, el := arr {
         fmt.Println(a, b)
       }
     } // O(n^2)
   } // O(n) + O(n^2) = O(n + n^2) = O(n^2)
   ```

## Exercises

### Exercise 1.

What is the time complexity for the following program?

```go
func sum(a, b int) int {
  return a + b
}
```

<details>
<summary>Answer</summary>

The running time is constant. Therefore, the time complexity is $O(1)$.

</details>

### Exercise 2.

What is the time complexity for the following program?

```go
func sum(l []int) int {
  total := 0
  for _, el := range l {
    total += el
  }
  return total
}
```

<details>
<summary>Answer</summary>

Assuming $n = $`len(l)`, the running time is linear, i.e. $T(n) = an + b$.
Therefore, the time complexity is $O(n)$.

</details>

### Exercise 4.

What is the time complexity for the following program?

```go
func sum(a [][]int) int {
  total := 0
  for i := range a {
    for j := range a[i] {
      total += a[i][j]
    }
  }
  return total
}
```

<details>
<summary>Answer</summary>

Assuming the input matrix has dimensions $m \times n$, the running time is $T(m, n) = a\cdot m \cdot n + b$. Therefore, the time complexity is $O(mn)$.

</details>

### Example 5.

What is the time complexity for the following program?

```go
func f(n int) int {
  a := 5
  for i := 0; i < n; i++ {
    a++
  }
  for i := 0; i < n; i++ {
    for j := 0; j < n; j++ {
      a++
    }
 }
 return a
}
```

<details>
<summary>Answer</summary>

The first loop has the time complexity $O(n)$. The second loop has the time complexity $O(n^2)$. The resulting complexity is $O(n) + O(n^2)= O(n^2)$.

</details>

### Example 6.

What is the time complexity for the following program?

```go
func isPowerOfTwo(n int) bool {
  if n == 0 {
    return false
  }
  for n != 1 {
    if n % 2 != 0 {
      return false
    }
    n /= 2
  }
  return true
}
```

<details>
<summary>Answer</summary>

The time complexity is $O(\log_2 n)$. This is because at every step we divide $n$ by $2$.

</details>