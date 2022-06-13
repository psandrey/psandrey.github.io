---
layout: page
title: Selection Sort
permalink: /sort/comparison_selection_sort/
---

* toc
{:toc}

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

## The Algorithm

**Selection sort** is a simple sorting algorithm based on comparison. It's somewhat similar to the next one - Insertion sort - but it performs worse in most cases. The algorithm builds the sorted sequence as a sorted stack from bottom up. Each step it finds the next item to stack it on top such that the stack remains ordered.

### Description

Lets assume we want to generate the items in ascending order and lets assume that we already found the first $$ m $$ items. Obviously, next item we need to stack is the minimum value from the remaining items. So, we need to have 2 loops: the outter loop to stack items and the inner loop to find the next item to stack (the minimum).

### Implementation

```cpp
void sort(vector<int> &a) {
    if (a.size() <= 1) return;

    for (int i = 0; i < (int)a.size() - 1; ++i) {
        int m = i;

        // find minimum from the remaining items
        for (int j = i + 1; j < (int)a.size(); ++j) {
            if (a(m) > a(j)) m = j;
        }

        // stack it
        swap(a(i), a(m));
    }
}
```
## Correctness

Initially, the stack is empty, so the outter loop starts from index $$ 0 $$ to $$ n - 1 $$ - basically it stacks all items. The inner loop find the first minimum item and swap it with the item from index 0. Now, the stack contains the first item and the inner loop finds the next minimum from the remaing items between index $$ 1 $$ and $$ n - 1 $$. So, the algorithm sort any given input.

## Complexity Analysis

### Time Complexity

 * **Worst Case** : $$ \theta(n^2) $$
 * **Average Case** : $$ \theta(n^2) $$
 * **Best Case**: $$ \theta(n^2) $$

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

There is no difference between **worst-case**, **average-case** and **best-case**, in all cases the inner loop runs $$ n - i - 1 $$ times for each item. \\
$$ T(n) = \sum_{i = 0}^{n-1} \left(\theta(n - i - 1) \right) = \theta\left(\frac{n(n-1)}{2} \right) = \theta(n ^ 2) $$. \\
\\
**Note**: Check the time complexity for Insertion sort to see the difference.

### Space Complexity (auxiliary)

 * $$ S(n) = \theta(1) $$.

---