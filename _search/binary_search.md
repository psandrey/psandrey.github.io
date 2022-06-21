---
layout: page
title: Binary search
permalink: /search/binary_search/
---

* toc
{:toc}

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

## Algorithm description

Given a monotonic function $$ f $$ and a $$ target $$, the **binary search** (aka. half-interval search or logarithmic search) algorithm finds the position $$ x $$ for which $$ f(x) = target $$. In case the function is discrete, then we have a discrete search space and we can find the precise position of the target (if exists) or in case the function is continuous (the set of real numbers is dense) we might not be able to find the exact target position, so we find some $$ x $$ such that $$ f(x) $$ is close to $$ target $$ with some aceptable tolerance. In both cases, the position is found by halving the search interval at each iteration based on the comparison between the middle item and the target.\\
**Note:** Basically, the search space is an interval of the domain of the function and the target value is an item of the codomain. \\
\\
In case you do not remember: a **monotonic function** is a function which is either nonincreasing or nondecreasing:
* monotonic:
  * increasing: $$ \forall x_1 \lt x_2 \Longrightarrow f(x_1) \le f(x_2) $$.
  * decreasing: $$ \forall x_1 \lt x_2 \Longrightarrow f(x_1) \ge f(x_2) $$.
* strictly monotonic:
  * strictly increasing: $$ \forall x_1 \lt x_2 \Longrightarrow f(x_1) \lt f(x_2) $$.
  * strictly decreasing: $$ \forall x_1 \lt x_2 \Longrightarrow f(x_1) \gt f(x_2) $$.

## Discrete search space

Lets assume we have a subsequence of the search space where we are looking for the $$ target $$: $$ \{low...high\} $$. We take the middle position of this subsequence $$ mid = (low + high)/2 $$ and we test to see if the element at $$ mid $$ position is the target. If not, we need to look into $$ \{low...mid\} $$ or $$ \{mid...high\} $$ subseqeunce, since the search space is ordered. So, we halved the search space. We do so until we either find the target or conclude that the target does not exists. \\
\\
The catch is the logarithmic time complexity: $$ log_2(\text{size of the search space}) $$. For example, the english dictionary has about 170K words and looking for a word takes at most 17 iterations: $$ log_2(170000) = 17 $$. A linear search in the worst case takes 170K iterations. \\
\\
**So, the binary search is an efficient algorithm for finding an item within an ordered list of items.** The list can be a log, a catalog, a dictionary... etc... as long as it is ordered, the algorithm works and performs well.

### Implementation:
```cpp
int search(vector<int>& a, int target) {
    int n = (int)a.size();

    int low = 0, high = n - 1;
    while (low <= high) {
        int middle = (low + high) / 2;

        if (target == a[middle]) return middle;
        else if (target < a[middle]) high = middle - 1;
        else low = middle + 1;
    }

    return -1;
}
```

## Continuous search space

Since we might not find the exact position of the target we need a way to decide to terminaate the search. So, we can stop if the difference between the value of $$ f(x) $$ and $$ target $$ is within aceptable boundaries or we can stop after a fixed number of interations (usually, a one or two hundreds is enough).

### Implementation:

Lets assume we have a function called $$ check $$ that returns true after $$ x $$ and false before. So, we need to find the closest value to the border between false and true. Also, we have a function called $$ terminate $$ which assesses whether the value we found is within acceptable limits or whether the number of iterations allowed has been consumed.

```cpp
double search(double low, double high, double target) {
    int iterations = 0;
    double middle = 0.0;
    while (terminate(iterations, middle, target)) {
      middle = (low + high) / 2.0;

      if (check(middle) == true) high = mid;
      else low = mid;

      iterations++;
    }

    return low;
}
```
## Complexity

Time complexity in worst-case and average-case is $$ log_2(n) $$ and in best-case is $$ O(1) $$. \\
Spaec complexity (auxiliary) is $$ O(1) $$.

## Practice

1. Find the index of a value in a sorted array.
2. Find the first and last occurrence of a given number in a sorted array.
3. Find the largest previous and the smallest following integer of a given number in a sorted array.
4. Find the square root of an integer.
5. Find the result of the division of two numbers.
6. Find the median of two sorted arrays.

## More reading

* [topcoder.com](https://www.topcoder.com/thrive/articles/Binary%20Search)
* [brilliant.org](https://brilliant.org/wiki/binary-search/)
* Skiena, The Algorithm Design Manual, 2nd ed, section 2.6, page 46.

---