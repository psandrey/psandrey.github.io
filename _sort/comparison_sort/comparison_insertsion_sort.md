---
layout: page
title: Insertion Sort
permalink: /sort/comparison_insertsion_sort/
---

```cpp
void sort(vector<int> &a) {
    if (a.size() <= 1) return;

    for (int i = 1; i < (int)a.size(); i++) {
        for (int j = i; j > 0; j--) {
            if (a[j] < a[j - 1]) swap(a[j], a[j - 1]);
            else break;
        }
    }
}
```

---