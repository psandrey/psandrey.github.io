---
layout: page
title: Heap Sort
permalink: /sort/comparison_heap_sort/
---

* toc
{:toc}

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

## The Algorithm
TODO

### Description
TODO

### Implementation
```cpp
void sort(vector<int>& a) {
    buildMaxHeap(a);

    int n = (int)a.size();
    for (int i = n - 1; i >= 0; i--) {
        swap(a[0], a[i]);
        sink(a, i, 0);
    }
}

void buildMaxHeap(vector<int>& a) {
    for (int i = 1; i < (int)a.size(); i++)
        rise(a, i);
}

void rise(vector<int>& heap, int i) {
    if (i == 0) return;

    int p = (i - 1) / 2;
    if (heap[p] < heap[i]) {
        swap(heap[p], heap[i]);
        rise(heap, p);
    }
}

void sink(vector<int>& heap, int n, int i) {
    if (i >= n) return;

    int l = 2 * i + 1, r = 2 * i + 2;
    int hi = i;
    if (l < n && heap[hi] < heap[l]) hi = l;
    if (r < n && heap[hi] < heap[r]) hi = r;

    if (hi != i) {
        swap(heap[hi], heap[i]);
        sink(heap, n, hi);
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