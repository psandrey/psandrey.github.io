---
layout: page
title: Radix Sort
permalink: /sort/distribution_sort/radix_sort/
---

```cpp
vector<int> sort(vector<int>& a, int radix, bool pigeon) {
    vector<int> sorted(a);
    int msb = logFloor(getMax(a), radix);
    
    // - sort the vector relative to digit d using a stable sort algorithm to preserve
    //   the relative position of items with identical previous digit
    // - stable sorting algorithms: counting sort, pigeonhole sort... etc).
    for (int d = 0; d <= msb; d++)
        if (pigeon) radixSortPigeon(sorted, radix, d);
        else sorted = radixSortCount(sorted, radix, d);

    return sorted;
}

// Note: Counting sort
vector<int> radixSortCount(vector<int>& a, int radix, int d) {
    int n = (int)a.size();
    int D = (int)pow(radix, d);
    
    // count occurrences
    vector<int> count(radix, 0);
    for (int i = 0; i < n; i++) {
        int digit = (a[i] / D) % radix;
        count[digit]++;
    }

    // shift indexes
    for (int i = 1; i < radix; i++)
        count[i] += count[i - 1];

    // distribute
    // stable sort: backwards to conserve relative position of identical items in the original array
    vector<int> sorted(n);
    for (int i = n - 1; i >= 0; i--) {
        int digit = (a[i] / D) % radix;
        sorted[count[digit] - 1] = a[i];
        count[digit]--;
    }

    return sorted;
}

// Note: Pigeonhole sort
void radixSortPigeon(vector<int>& a, int radix, int d) {
    int n = (int)a.size();
    int D = (int)pow(radix, d);

    // items to holes
    vector<list<int>> holes(radix, list<int>());
    for (int i = 0; i < (int)a.size(); i++) {
        int b = (a[i] / D) % radix;
        holes[b].push_back(a[i]);
    }

    // distribute
    // stable sort: backwards to conserve relative position of identical items in the original array
    int j = n - 1;
    for (int i = radix - 1; i >= 0; i--) {
        while (!holes[i].empty()) {
            a[j--] = holes[i].back();
            holes[i].pop_back();
        }
    }
}

int getMax(vector<int>& a) {
    int m = INT_MIN;
    for (int i = 0; i < (int)a.size(); i++)
        m = max(m, a[i]);

    return m;
}

int logFloor(int x, int base) {
    return (int)(log(x) / log(base));
}
```

---