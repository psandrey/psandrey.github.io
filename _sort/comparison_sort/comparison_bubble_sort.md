---
layout: page
title: Bubble Sort
permalink: /sort/comparison_bubble_sort/
---

```cpp
void sort(vector<int>& a) {
    if (a.size() <= 1) return;

    for (int i = 0; i < (int)a.size(); i++) {

        bool swapped = false;
        for (int j = 0; j < (int)a.size() - 1; j++) {
            if (a[j] > a[j + 1]) {
                swap(a[j], a[j + 1]);
                swapped = true;
            }
        }

        if (!swapped) break;
    }
}
```

---