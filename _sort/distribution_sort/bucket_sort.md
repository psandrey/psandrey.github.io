---
layout: page
title: Bucket Sort
permalink: /sort/distribution_sort/bucket_sort/
---

* toc
{:toc}

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

<pre>/ <a onclick="window.history.back()" style="cursor:pointer;"> Back </a> / <a href="/"> Home </a> / </pre>

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

## The Algorithm

**Bucket sort** is a sorting algorithm that performs in linear time when the input is uniformly distributed over the interval $$ [0,1) $$.

### Description

The interval is divided into $$ n $$ buckets, and data is distributed to these buckets. Since data is uniformly distributed, we do not expect many numbers to fall into the same bucket. After distribution, each bucket is sorted and then the data is globally sorted by concatenating the buckets in order.

\\
Note: If the numbers are integers uniformly distributed over some range, then the range can be reduced to $$ [0, 1) $$ by dividing each number to the size of that range.

### Implementation

```cpp
void sort(vector<int>& a, int M) {
    int n = (int)a.size();
    vector<list<int>> bucket(n, list<int>());

    // distribute into buckets
    for (int i = 0; i < n; i++) {
        int b = (int)floor(((double)a[i] / (double)M) * (double) n);
        bucket[b].push_back(a[i]);
    }

    // local sort each bucket
    for (int i = 0; i < n; i++)
        if (!bucket[i].empty()) bucket[i].sort();

    // concatenate buckets in order
    int j = 0;
    for (int i = 0; i < n; i++) {
        while (!bucket[i].empty()) {
            a[j++] = bucket[i].front();
            bucket[i].pop_front();
        }
    }
}
```

## Correctness

Entire set is traversed and all items are placed into buckets. Since the buckets themselves are ordered by construction, if two items are in two different buckets, then the items are ordered. If two items are in the same bucket then they are sorted because the buckets are sorted before concatenation. Since the buckets are concatenated in sorted order and each bucket contains sorted elements, then the algorithm produces a sorted sequence for any given input.

## Complexity Analysis

### Time Complexity

In the worst case, the numbers fall into the same bucket, and the complexity will be driven by the complexity of the sorting algorithm, so $$ T(n) = O(n^2) $$ if insertion is used or $$ T(n) = O(n \cdot logn) $$ if qsort is used.

\\
In the average case and best case, the numbers are evenly distributed over the buckets and $$ n \sim k $$, so $$ T(n) = O(n) $$.

\\
**Note**: In CLRS, section 8 can be found a detailed proof for average case using random variable indicators.

### Space Complexity (auxiliary)

We need a list of buckets of size $$ n + k $$, so $$ S(n) = O(n + k) $$ where $$ k $$ is the number of buckets and $$ n $$ is the size of the original array.

## Stability

Bucket sort is stable, if the underlying sort is also stable, as equal keys are inserted in order to each bucket. In the implementation above the buckets are sorted using qsort which is unstable, but if insertion sort is used instead, then the implementation above becomes stable. 

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

<pre>/ <a onclick="window.history.back()" style="cursor:pointer;"> Back </a> / <a href="/"> Home </a> / </pre>

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">