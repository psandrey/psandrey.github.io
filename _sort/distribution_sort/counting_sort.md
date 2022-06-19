---
layout: page
title: Counting Sort
permalink: /sort/distribution_sort/counting_sort/
---

```cpp
vector<int> sort(vector<int>& a, int k) {
    vector<int> counter(k + 1, 0);
    vector<int> b(a.size());

    // count occurrences
    for (int i = 0; i < (int)a.size(); i++)
        counter[a[i]]++;

    // shift indexes
    for (int i = 1; i <= k; i++)
        counter[i] += counter[i - 1];

    // distribute
    // stable sort: backwards to conserve relative position of identical items in the original array
    // Note: e.g. stability is needed it for radix sort
    for (int i = (int)a.size() - 1; i >= 0; i--) {
        b[counter[a[i]] - 1] = a[i]; // -1 because vector is from 0
        counter[a[i]]--;
    }

    return b;
}
```

---