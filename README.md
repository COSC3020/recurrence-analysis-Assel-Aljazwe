[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/OlW38W4k)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.


## Analysis of the $mystery$ Function's Runtime

The runtime analysis of a recursive function, named $mystery$, to determine its computational complexity as a function of $n$. 

### Function Overview

The $mystery$ function is defined as follows:

- It returns immediately if $n <= 1$.
- It makes three recursive calls to itself with $n/3$ as the new argument.
- It executes a triple-nested loop that iterates $n * n$ times in the outer loop, $n$ times in the middle loop, and $n * n$ times in the innermost loop, leading to a total of $n^5$ operations.

### Recurrence Relation Derivation

Based on the function's structure, we establish the following recurrence relation for its runtime $T(n)$:

$T(n) = 3T(n/3) + n^5$

### Manual Expansion and Analysis

1. **Initial Expansion:**
   - At the first level for $n > 1$, the function's runtime is: $T(n) = 3T(n/3) + n^5$.

2. **Further Expansion:**
   - Expanding the recursive calls further, we observe the pattern: $T(n) = 9T(n/3^2) + 3(n/3)^5 + n^5$.

3. **Generalization to i-th Level:**
   - Continuing this pattern up to the $i-th$ level, where $i$ is determined by when $n$ has been reduced to $1$ or less, we arrive at: $T(n) = 3^iT(n/3^i) + n^5 * Σ(1/3^(5k))$ from $k=0$ to $i-1$.

### Solving the Recurrence

- The recursion concludes when $n/3^i ≤ 1$, implying $i = log_3(n)$.
- The series $Σ(1/3^(5k))$ from $k=0$ to $i-1$ converges to a constant factor, indicating that the loops' contribution of $n^5$ dominates the runtime.

### Big O Bound Conclusion

Given the significant impact of the triple-nested loops compared to the recursive calls in the mystery function, we determine its Big O runtime complexity to be
$O(n^5)$ Highlighting that the function's execution time scales with the fifth power of the input size n, primarily due to these loops.


