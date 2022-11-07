---
layout: page
title: Counting Sort
permalink: /sort/distribution_sort/counting_sort/
---

* toc
{:toc}

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

<pre>/ <a onclick="window.history.back()" style="cursor:pointer;"> Back </a> / <a href="/"> Home </a> / </pre>

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

## The Algorithm

**Counting sort** is a sorting algorithm used to sort a collection of items by their keys that are non-negative small integers. The values of these keys fall within a certain upper limit given as input along with the set of items.

### Description

In short, the algorithm counts the values found in the given set and then places them in sorted order back into the set. Thus, a vector of counters is used for counting, one counter for each value between 0 and k (where k is the acceptable upper limit). After counting, each counter contains the number of values equal to the position of the counter in the vector of counters. For example, the 5th counter contains all values equal to 5 found in the set. Then this vector of counters must be transformed into vector of indexes so that we can place the values in ascending order. Thus, all counters representing smaller values are added to the current counter and now the counter contains the number of values equal to or smaller than the position of the counter in the vector. For example, all counters representing the number of occurrences of values between $$ 0 $$ and $$ x_1 $$ are added to the counter $$ c_{x_{1}} $$ , which represents the number of occurrences of the value $$ x_1 $$. Now that we have the indexes of the values in sorted order, all we have to do is place the values at the corresponding index.

#### Stability

To preserve the relative position of identical elements from the original array, when values are counted the array is traversed from left to right, and when values are placed back in sorted order, the array is traversed from right to left . Think of it as a stack, once a number is stacked in an order, when it is unstacked, the order is reversed, so the array must be traversed in reverse to keep the order.

### Implementation

```cpp
void sort(vector<int>& a, int k) {
    int n = (int)a.size();
    if (a.size() <= 1) return;

    vector<int> b(a.size());
    vector<int> counter(k + 1, 0);
    
    // distribution: values in the set are counted and the counter contains
    // the number of values less than i
    for (int i = 0; i < n; i++)
        counter[b[i]]++;

    // counters are transformed into indexes and now the counter contains
    // the number of values equal or less than i
    for (int i = 1; i <= k; i++)
        counter[i] += counter[i - 1];

    // place items in sorted order
    // Note: preserve the relative position of identical items
    // from the original array (stability)
    for (int i = n - 1; i >= 0; i--) {
        int j = counter[b[i]] - 1;
        counter[b[i]]--;

        a[j] = b[i];
    }
}
```

## Complexity Analysis

### Time Complexity

The algorithm has 3 loops, 2 loops to $$ n $$ and one loop to $$ k $$, so $$ T(n) = \Theta(n + k) $$, where $$ n $$ is the size of the array and $$ k $$ is the upper limit of acceptable values.

### Space Complexity (auxiliary)

The algorithms needs the array of counters, which is of size $$ k $$ and it also needs to copy the original set, which is of size $$ n $$, so $$ S(n) = \Theta(n + k) $$.

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

<pre>/ <a onclick="window.history.back()" style="cursor:pointer;"> Back </a> / <a href="/"> Home </a> / </pre>

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">