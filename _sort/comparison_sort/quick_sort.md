---
layout: page
title: Quick Sort
permalink: /sort/comparison_sort/quick_sort/
---

* toc
{:toc}

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

## The Algorithm
TODO

### Description
TODO

### Implementation

#### Recursive version

```cpp
void quicksort(vector<int>& a, int s, int e) {
    if (e - s <= 1) return;

    int p = partition(a, s, e);
    quicksort(a, s, p);
    quicksort(a, p + 1, e);
}

int partition(vector<int>& a, int s, int e) {
    /* a[s] is the pivot
        * For Randomized QuickSort, chose a random pivot between s and e and
        * swap it with a[s]; the partitioning remains as is. */
    int p = s + rand() % (e - s);
    swap(a[s], a[p]);
    
    int i = s;
    for (int j = s; j < e; j++) {
        if (a[j] < a[s]) swap (a[++i], a[j]);
    }
    swap (a[s], a[i]);

    return i;
}
```

#### Iterative version
```cpp
void quicksort(vector<int>& a) {
    if (a.size() <= 1) return;
    stack<pair<int, int>> st;
    st.push(make_pair(0, a.size()));
    
    // preorder traversal of indexes
    while (!st.empty()) {
        pair<int, int> n = st.top(); st.pop();
        int s = n.first, e = n.second;

        int p = partition(a, s, e);
        if (e - (p + 1) > 1) st.push(make_pair(p + 1, e));
        if (p - s > 1) st.push(make_pair(s, p));
    }
}
```
## Correctness
TODO

## Complexity Analysis
TODO

### Time Complexity
TODO

### Space Complexity (auxiliary)
TODO

---