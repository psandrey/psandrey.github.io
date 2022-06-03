---
layout: page
title: Bogosort
permalink: /sort/comparison_bogosort/
---

```cpp
void sort(vector<int>& a) {
    if (a.size() <= 1) return;

    while (!is_sorted(a)) {
        shuffle(a);
    }
}

bool is_sorted(vector<int>& a) {
    bool sorted = true;

    for (int i = 1; i < (int)a.size(); i++)
        if (a[i] < a[i - 1]) {
            sorted = false;
            break;
        }

    return sorted;
}

void shuffle(vector<int>& a) {
    for (int i = 0; i < (int)a.size(); i++)
        swap(a[i], a[rand() % n]);
}
```

---