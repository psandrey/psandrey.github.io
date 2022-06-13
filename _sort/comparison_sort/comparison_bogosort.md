---
layout: page
title: Bogosort
permalink: /sort/comparison_bogosort/
---

* toc
{:toc}

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

## The Algorithm

**Bogosort** (also known as shotgun sort, stupid sort, random sort, permutation sort, or slowsort) is a sorting algorithm based on the "trial and error" paradigm (varied attempts which are continued until success, or until the practicer stops trying), (source: wikipedia). 

### Description

Probably this is the most useless sorting algorithm, because it is extremly inefficient. There are 2 versions of this algorithm: one that enumerates all permutations until it finds the one that has all the items sorted and one randomized version that might never hit the sorted sequence. I would say that this algorithm is interesting from theoretical point of view rather than real applications.

Below there is a simple implementation of the randomized version, where we generate a permutation and then we check to see if the sequence is sorted. We do so, until we find the permutation with the sorted sequence or until "the end of time" (because, each permutation is generated independently and with equal probability, so there is no certainty that the sorted permutation is hit).

### Implementation

```cpp
void sort(vector<int>& a) {
    if (a.size() <= 1) return;

    while (!is_sorted(a)) {
        shuffle(a);
    }
}

bool is_sorted(vector<int>& a) {
    bool sorted = true;

    for (int i = 1; i < (int)a.size(); ++i)
        if (a[i] < a[i - 1]) {
            sorted = false;
            break;
        }

    return sorted;
}

void shuffle(vector<int>& a) {
    for (int i = 0; i < (int)a.size(); ++i)
        swap(a[i], a[rand() % n]);
}
```

## Correctness

Certainly one of the permutations has the items in sorted order. Each time a sequence is generated, it is checked by comparing the order of adjacent itmes. If all the adjacent items are ordered, then we found the sorted permutation, if not, then another sequence is generated. So, if the sorted permutation is hit, then the algorithm ends and the correct result is produced.

## Complexity Analysis

### Time Complexity

 * **Worst Case** : $$ O(\infty) $$ (since this algorithm has no upper bound)
 * **Average Case** : $$ O(n*n!) $$
 * **Best Case**: $$ O(n) $$ (if the given sequence is already sorted)

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

**TODO**: *proof in progress...* \\
\\
**Note**: comprehensive proof : https://sites.math.washington.edu/~morrow/336_13/papers/max.pdf

### Space Complexity (auxiliary)

 * $$ S(n) = \theta(1) $$.

---