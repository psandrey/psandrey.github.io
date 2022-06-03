---
layout: page
title: Bucket Sort
permalink: /sort/distribution_bucket_sort/
---

If elementes of the set are integers and uniformly distributed over some given interval:

```cpp
void sort(vector<int>& a) {
    int n = (int)a.size();
    vector<list<int>> bucket(n, list<int>());

    // the maximum number will go to bucket (n - 1)
    int M = getMax(a);

    // distribute into buckets
    for (int i = 0; i < n; i++) {
        // hash: divide then multiply to avoid overflow
        int b = (int)floor(((double)a[i] / M) * ((double)n - 1.0));
        bucket[b].push_back(a[i]); 
    }

    // sort each bucket
    for (int i = 0; i < n; i++)
        if (!bucket[i].empty()) bucket[i].sort();

    // reconstruct the set from in-order buckets
    int j = 0;
    for (int i = 0; i < n; i++)
        if (!bucket[i].empty()) {
            list<int>::iterator it_i;
            for (it_i = bucket[i].begin(); it_i != bucket[i].end(); it_i++)
                a[j++] = *it_i;
        }
}

int getMax(vector<int>& a) {
    int m = INT_MIN;
    for (auto x : a) m = max(m, x);
    return m;
}
```

If elementes of the set are uniformly distributed over the interval $$ [0, 1) $$ :

```cpp
void sort(vector<double>& a) {
    int n = (int)a.size();
    vector<list<double>> bucket(n, list < double > ());

    // distribute into buckets
    for (int i = 0; i < n; i++) {
        int b = (int)floor(a[i] * n);
        bucket[b].push_back(a[i]);
    }

    // sort each bucket
    for (int i = 0; i < n; i++)
        if (!bucket[i].empty()) bucket[i].sort();

    // reconstruct a from in-order buckets
    int j = 0;
    for (int i = 0; i < n; i++)
        if (!bucket[i].empty()) {
            list<double>::iterator it_i;
            for (it_i = bucket[i].begin(); it_i != bucket[i].end(); it_i++)
                a[j++] = *it_i;
        }
}
```

---