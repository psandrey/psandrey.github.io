---
layout: page
title: Pigeonhole Sort
permalink: /sort/distribution_sort/pigeonhole_sort/
---

* toc
{:toc}

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

<pre>/ <a onclick="window.history.back()" style="cursor:pointer;"> Back </a> / <a href="/"> Home </a> / </pre>

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

## The Algorithm

**Pigeonhole sort** is a sorting non-comparison algorithm suitable for sorting lists of elements, where the size of the list and the range of the possible keys are approximately the same.

### Description

**Pigeonhole principle**: if $$ n + 1 $$ pigeon occupy n holes, then same hole must have at least 2 pigeon.

\\
This algorithm is similar with counting sort and bucket sort:
- counting sort: builds an auxiliary array to compute the final destination, while pigeonhole sort moves items twice: once in the bucket and again into the final destination. One more thing, counting sort is used for indexed collection only, while pigeonhole sort can be used also for lists.
- bucket sort: if the range of the keys is much larger than the size of the list, then bucket sort is more efficient in space and time complexity. Values are distributed to buckets that are sorted by nature for pigeonhole sort and must be sorted for bucket sort since a bucket can contain keys with different values. So, bucket sort can be considered a generalization of pigeonhole sort.


\\
In short, the algorithm distribute the values into the proper bucket (pigeon hole) and then place values back from buckets (pigeon holes) into sorted order. First, we need to compute the range of all possible values. This range is obviously equal to the maximum value in the set minus minimum value. So, to distribute data we need an array of size *range* of lists, similar with bucket sort. Each list accumulates elements with the same value. After distribution, the only thing we need to do is to traverse this array of lists in increasing order relative to the *range* and place back the values in sorted order.

#### Stability

To preserve the relative position of identical elements from the original array, the elements are stacked in pigeon holes, and when are unstacked, the order is reversed, so the pigeon holes must be traversed in reverse to keep the order. So, Pigeonhole sort is stable. 

### Implementation

```cpp
void sort(vector<int>& a) {
    if (a.size() <= 1) return;
    int m = getMin(a), M = getMax(a);
    int range = M - m + 1;
    vector<vector<int>> holes(range, vector<int>());

    // distributed items to holes
    for (int i = 0; i < (int)a.size(); i++)
        holes[a[i] - m].push_back(a[i]);

    // gather items in sorted order
    int j = (int)a.size() - 1;
    for (int i = range - 1; i >= 0; i--) {
        while (!holes[i].empty()) {
            a[j--] = holes[i].back();
            holes[i].pop_back();
        }
    }
}
```

## Complexity Analysis

### Time Complexity

The algorithm have 2 loops, one of size $$ range + n $$ and one of size $$ n $$, so $$ T(n) = O(n + range) $$. If $$ range \sim n $$, then $$ T(n) = O(n) $$.

### Space Complexity (auxiliary)

The size of the array of lists is $$ range + n $$, so $$ S(n) = O(n + range) $$. If $$ range \sim n $$, then $$ S(n) = O(n) $$.

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

<pre>/ <a onclick="window.history.back()" style="cursor:pointer;"> Back </a> / <a href="/"> Home </a> / </pre>

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">