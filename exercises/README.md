# Home assignment

## Standard (100%)

1. https://codeforces.com/problemset/problem/466/A
2. https://codeforces.com/problemset/problem/581/A
3. https://codeforces.com/problemset/problem/122/A

## Extra (up to 100%)

### Points

- 100% for time complexity `O(N)`, space complexity `O(1)` (no allocations) 
- Any other implementation extra 50%.

### Prototype

```go
func rearrange(s []int, pivot int) (i int)
```

### Problem

Implement the function `rearrange` which accepts the slice and the index named
`pivot`. The function must rearrange elements in the slice into two segments:

1. Elements with values lower than `s[pivot]`.
2. Everything else.

The function returns the index of the split such as for every element value of
`s[:i]` is lower than `s[pivot]` and `s[i:]` is everything else.

Note: Your slice values may be different depending on the algorithm that you
come up with. But the returned `i` must be the same.

### Example 1 (no repeated elements)

```go
s := []int{8, 4, 1, 0, 5, 9, 3, 7, 2, 6}
fmt.Println(rearrange(s, 4), s) // Output: 5 [2 4 1 0 3 5 9 7 8 6]
```

### Example 2 (repeated elements)

```go
s := []int{9, 6, 1, 7, 5, 9, 6, 5, 2, 6}
fmt.Println(rearrange(s, 9), s) // Output: 4 [2 5 1 5 6 9 6 7 6 9]
```

### Example 3 (empty left side)

```go
s := []int{9, 6, 1, 7, 5, 9, 6, 5, 2, 0}
fmt.Println(rearrange(s, 9), s) // Output: 0 [0 6 1 7 5 9 6 5 2 9]
```
