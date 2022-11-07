---
layout: page
title: Bubble Sort
permalink: /sort/comparison_sort/bubble_sort/
---

* toc
{:toc}

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

<pre>/ <a onclick="window.history.back()" style="cursor:pointer;"> Back </a> / <a href="/"> Home </a> / </pre>

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

## The Algorithm

**Bubble sort** (aka sinking sort) is probably the simplest sorting algorithm based on comparison. The idea is to compare adjacent items and then swap their positions if they are not in sorted order. The sequence is sweeped until all adjacent items are in sorted order and no positions are swapped. 

### Description

There can be at most $$ n $$ sweep, since we have $$ n $$ items to sink. Each item can sink up to $$ n - 1 $$ positions. So, we need two loops: the outter loop which represents the number of sweeps and the inner loop which sinks each item to its correct position. For each sweep we need a flag which is set if any positions were swapped, so that we know if another sweep is needed and check again. In the inner loop we check the order of every 2 adjacent items and we swap them if they are not ordered. If we swap, then we also set the flag. After the inner loop ends, in the outter loop the flag is checked and if it is not set then the algorithm ends, otherwise we sweep again.

### Implementation

```cpp
void sort(vector<int>& a) {
    if (a.size() <= 1) return;
    bool flag = true;

    while(flag) {
        flag = false;
        for (int j = 1; j < (int)a.size(); ++j) {
            if (a[j] < a[j - 1]) {
                swap(a[j], a[j - 1]);
                flag = true;
            }
        }
    }
}
```

## Correctness

There are at most $$ n $$ sweeps since there are at most $$ n $$ items that needs to sink to the right place and each item can skink at most $$ n $$ positions. So, the 2 loops produce the sorted sequence for any given sequence.

## Complexity Analysis

### Time Complexity

 * **Worst Case** : $$ \theta(n^2) $$
 * **Average Case** : $$ \theta(n^2) $$
 * **Best Case**: $$ \theta(n) $$

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

In the **wors-case**, the outter loop length is n, so the inner loop runs n times:
$$ T(n) = \theta(n^2) $$. \\
\\
In the **average-case** (when the sequence is half sorted), the outter loop length is $$ \frac{n}{2} + 1 $$, so the inner loop runs $$ \frac{n}{2} + 1 $$ times:
$$ T(n) = (\frac{n}{2} + 1) * n = \theta(n^2) $$.\\
\\
In the **best-case** (when the sequence is already sorted), the outter length ia 1, so inner loop runs once:
$$ T(n) = \theta(n) $$.

### Space Complexity (auxiliary)

 * $$ S(n) = \theta(1) $$.

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

<pre>/ <a onclick="window.history.back()" style="cursor:pointer;"> Back </a> / <a href="/"> Home </a> / </pre>

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">