---
layout: page
title: Insertion Sort
permalink: /sort/comparison_insertsion_sort/
---

* toc
{:toc}

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

## The Algorithm

**Insertion sort** is another simple sorting algorithm based on comparison, but compared with the provious three, this one it is used in real applications. It maintains a sorted subsequence in which it inserts each item in its proper place, and thus produces the sorted sequence. The analogy I've seen most often is with the way people sort the playing cards... a good one.

### Description

Lets assume that we have sorted the subsequence from index $$ 0 $$ to some index $$ i-1 \lt n - 1 $$ and the subsequence from $$ i $$ to $$ n - 1 $$ it is not. As the algorithm suggest, we need to insert one by one all items from  $$ i $$ to $$ n - 1 $$ into the sorted subsequence to their rightful place. First, we insert the i-th item by swapping it with all items to its left that are bigger then him. Then, we need to insert the next item in the same way (basically, we do the same with all items up to $$ n - 1 $$). See an example below:\\
![pic_01](/sort/comparison_sort/img/comparison_sort_insertion_sort_1.png){:height="220pt" style="float: left"}
<br><br>
The i-th item (index 4, number 3) is inserted into the sorted subsequence (index 0 to 3).\\
There are 3 swaps until 3 is inserted between 2 and 5: (9,3), (8,3) and (5,3).

{:style="clear:both"}
![pic_02](/sort/comparison_sort/img/comparison_sort_insertion_sort_2.png){:height="190pt"}
![pic_03](/sort/comparison_sort/img/comparison_sort_insertion_sort_3.png){:height="190pt"}
![pic_04](/sort/comparison_sort/img/comparison_sort_insertion_sort_4.png){:height="190pt"}

### Implementation

```cpp
void sort(vector<int> &a) {
    if (a.size() <= 1) return;

    for (int i = 1; i < (int)a.size(); ++i) {
        for (int j = i; j > 0; --j) {
            if (a[j - 1] > a[j]) swap(a[j], a[j - 1]);
            else break;
        }
    }
}
```

## Correctness

Initially, the sorted subsequence contains only the item from index $$ 0 $$ and the outter loop runs for all items starting with second index up to $$ n - 1 $$, thus all items are inserted. The inner loop swap i-th item at most $$ i - 1 $$ times, so that the subsequence is kept invariant. So, the algorithm sort any given input.

## Complexity Analysis

### Time Complexity

 * **Worst Case** : $$ \theta(n^2) $$
 * **Average Case** : $$ \theta(n^2) $$
 * **Best Case**: $$ \theta(n) $$

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

In the **worst-case**, the given sequence is sorted in opposite way, therefore the inner loop runs i times for each item. \\
$$ T(n) = \sum_{i = 1}^{n-1} \left(\theta(i) \right) =\theta\left(\frac{n(n-1)}{2}  \right) = \theta(n ^ 2) $$. \\
\\
In the **average-case**, each item is inserted in the middle of the sorted sequence, thus only half of the sequence is moved, or in other words, the inner loop runs $$ \frac{i}{2} $$ times for each item. \\
$$ T(n) = \sum_{i = 1}^{n-1} \left(\theta\left( \frac{i}{2} \right) \right) =\theta\left(\frac{n(n-1)}{4}  \right) = \theta(n ^ 2) $$. \\
\\
In the **best-case**, the given sequence is sorted, so the inner loop runs only 1 time. \\
$$ T(n) = \sum_{i = 1}^{n-1} \left( \theta(1) \right) = \theta(n) $$.

### Space Complexity (auxiliary)

 * $$ S(n) = \theta(1) $$.

---