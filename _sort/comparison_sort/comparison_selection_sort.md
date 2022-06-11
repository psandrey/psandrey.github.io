---
layout: page
title: Selection Sort
permalink: /sort/comparison_selection_sort/
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
void sort(vector<int> &a) {
    if (a.size() <= 1) return;

    for (int i = 0; i < (int)a.size() - 1; i++) {
        int m = i;
        for (int j = i + 1; j < (int)a.size(); j++) {
            if (a[m] > a[j]) m = j;
        }
        swap(a[i], a[m]);
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