---
layout: page
title: Pigeonhole Sort
permalink: /sort/distribution_sort/pigeonhole_sort/
---


```cpp
void sort(vector<int>& a) {
    if (a.size() <= 1) return;
    int m = getMin(a), M = getMax(a);
    int range = M - m + 1;
    vector<vector<int>> holes(range, vector<int>());

    // items to holes
    for (int i = 0; i < (int)a.size(); i++)
        holes[a[i] - m].push_back(a[i]);

    // distribute
    // stable sort: backwards to conserve relative position of identical items in the original array
    int j = (int)a.size() - 1;
    for (int i = range - 1; i >= 0; i--) {
        while (!holes[i].empty()) {
            a[j--] = holes[i].back();
            holes[i].pop_back();
        }
    }
}

int getMin(vector<int>& a) {
    int m = INT_MAX;
    for (int i = 0; i < (int)a.size(); i++)
        m = min(m, a[i]);

    return m;
}

int getMax(vector<int>& a) {
    int m = INT_MIN;
    for (int i = 0; i < (int)a.size(); i++)
        m = max(m, a[i]);

    return m;
}
```

---