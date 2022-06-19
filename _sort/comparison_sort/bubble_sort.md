---
layout: page
title: Bubble Sort
permalink: /sort/comparison_sort/bubble_sort/
---

* toc
{:toc}

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

## The Algorithm

**Bubble sort** (aka sinking sort) is probably the simplest sorting algorithm based on comparison. The idea is to compare adjacent items and then swap their positions if they are not in sorted order. The sequence is sweeped until all adjacent items are in sorted order and no positions are swapped. 

### Description

There can be at most $$ n $$ sweep, since we have $$ n $$ items to sink. Each item can sink up to $$ n $$ positions. So, we need two loops: the outter loop which represents the number of sweeps and the inner loop which sinks each item to its correct possition. For each sweep we need a flag which is set if any positions were swapped, so that we know if another sweep is needed. In the ineer loop we check the order of every 2 adjacent items and if it is wrong then we swap them. If we swap then we also set the flag. After the inner loop ends, in the outter loop the flag is checked and if it is set then the algorithm ends, otherwise we reset the flag and sweep again.

### Implementation

```cpp
void sort(vector<int>& a) {
    if (a.size() <= 1) return;

    for (int i = 0; i < (int)a.size(); ++i) {

        bool swapped = false;
        for (int j = 0; j < (int)a.size() - 1; ++j) {
            if (a[j] > a[j + 1]) {
                swap(a[j], a[j + 1]);
                swapped = true;
            }
        }

        if (!swapped) break;
    }
}
```

## Correctness

There are at most $$ n $$ sweeps since there are at most $$ n $$ items that needs to sink to the right place and each item can sking at most $$ n $$ positions. So, the 2 loops produce the sorted sequence for any given sequence.

## Complexity Analysis

### Time Complexity

 * **Worst Case** : $$ \theta(n^2) $$
 * **Average Case** : $$ \theta(n^2) $$
 * **Best Case**: $$ \theta(n) $$

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

In the **wors-case**, the outter loop runs n times. The inner loop runs n-1 times for the first outter loop, n-2 times for the second outter loop and so on.
$$ T(n) = (n-1) + (n-2) + (n-3) + ... + 1 + 1 = \frac{n(n-1)}{2} + 1 = \theta(n^2) $$. \\
\\
In the **average-case** (when the sequence is half sorted), the outter loop runs $$ \frac{n}{2} + 1 $$ times and the intter loop runs the same as before (n-1 times for the first outter loop, n-2 times for the second outter loop and so on).
$$ T(n) = (n-1) + (n-2) + (n-3) + ... + \frac{n}{2} + 1 = \theta(n^2) $$.\\
\\
In the **best-case** (when the sequence is already sorted). the outter and inner loop runs once.
$$ T(n) = \theta(1) $$.

### Space Complexity (auxiliary)

 * $$ S(n) = \theta(1) $$.

---