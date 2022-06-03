---
layout: page
title: Merge Sort
permalink: /sort/comparison_merge_sort/
---

Recursive version:

```cpp
void sort(vector<int>& a, int s, int e) {
    if (e - s <= 1) return;

    int m = (s + e) / 2;
    sort_r(a, s, m);
    sort_r(a, m, e);
    merge(a, s, m, e);
}

void merge(vector<int>& a, int s, int m, int e) {
    vector<int> L(a.begin() + s, a.begin() + m);
    vector<int> R(a.begin() + m, a.begin() + e);

    // merge L and R so that a from s to e is sorted
    int k = s, i = 0, j = 0;
    while (i < (int)L.size() && j < (int)R.size())
        if (L[i] < R[j]) a[k++] = L[i++];
        else a[k++] = R[j++];
    
    // add tail of L or R (if any)
    while (i < (int)L.size()) a[k++] = L[i++];
    while (j < (int)R.size()) a[k++] = R[j++];
}
```

Iterative version:

```cpp
void sort(vector<int>& a) {
    if (a.size() <= 1) return;
    stack<pair<int, int>> st; st.push(make_pair(0, a.size()));
    pair<int, int> p = make_pair(-1, -1);

    // postorder traversal of indexes
    while (!st.empty()) {
        pair<int, int> n = st.top();
        int s = n.first, e = n.second;

        if (e - s <= 1) st.pop();
        else {
            int m = (s + e) / 2;

            // if the right side was previous visited, then both halves are sorted, so merge them 
            if (p.first == m && p.second == e) {
                merge(a, s, m, e);
                st.pop();
            }
            else {
                st.push(make_pair(m, e));
                st.push(make_pair(s, m));
            }
        }

        p = n;
    }
}
```

---