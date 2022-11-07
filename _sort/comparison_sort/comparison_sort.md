---
layout: page
title: Comparison Sorting Algorithms
permalink: /sort/comparison_sort/
---

<pre>/ <a onclick="window.history.back()" style="cursor:pointer;"> Back </a> / <a href="/"> Home </a> / </pre>

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

Comparison sorting is a class of sorting algorithms that relies on comparison operations (e.g. three way comparison ) to determine the order of two items in a set. In essence, these algorithms return a permutation of the original set so that the elements are ordered:
  * **Input**: a set of n-items: $$ a_1, a_2, a_3, ... , a_n $$
  * **Output**: a permutation: $$ a_{1}^{`}, a_{2}^{`}, a_{3}^{`}, ... , a_{n}^{`} $$ such that $$ a_{1}^{`} \leq a_{2}^{`} \leq a_{3}^{`}\leq ... \leq a_{n}^{`} $$
  
 <hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

  * <a href="/sort/comparison_sort/bogosort/"> Bogosort (aka. Shotgun sort, Stupid sort, Random sort, Permutation sort) </a>
  * <a href="/sort/comparison_sort/bubble_sort/"> Bubble Sort </a>
  * <a href="/sort/comparison_sort/selection_sort/"> Selection Sort </a>
  * <a href="/sort/comparison_sort/insertion_sort/"> Insertion Sort </a>
  * <a href="/sort/comparison_sort/merge_sort/"> Merge Sort </a>
  * <a href="/sort/comparison_sort/quick_sort/"> Quicksort </a>
  * <a href="/sort/comparison_sort/heap_sort/"> Heapsort </a>

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

**Complexity Table**:

| Algorithm      | T worst case              | T  avg case               | T best case                  | Space aux. | Stable  |
|----------------|---------------------------|---------------------------|------------------------------|------------|---------|
| Bogosort       | $$ O(\infty) $$           | $$ O((n+1)!) $$           | $$ O(n) $$                | $$ O(1) $$    |   no    |
| Bubble sort    | $$ O(n^2) $$              | $$ O(n^2) $$              | $$ O(n) $$                | $$ O(1) $$    |   yes   |
| Selection sort | $$ O(n^2) $$              | $$ O(n^2) $$              | $$ O(n^2) $$              | $$ O(1) $$    |   no    |
| Insertion sort | $$ O(n^2) $$              | $$ O(n^2) $$              | $$ O(n) $$                | $$ O(1) $$    |   yes   |
| Merge sort     | $$ O(n \cdot log_{2}n) $$ | $$ O(n \cdot log_{2}n) $$ | $$ O(n \cdot log_{2}n) $$ | $$ O(n) $$    |   yes   |
| Quicksort      | $$ O(n^2) $$              | $$ O(n \cdot log_{2}n) $$ | $$ O(n \cdot log_{2}n) $$ | $$ O(n) $$    |   no    |
| Heapsort       | $$ O(n \cdot log_{2}n) $$ | $$ O(n \cdot log_{2}n) $$ | $$ O(n \cdot log_{2}n) $$ | $$ O(1) $$    |   no    |

{:style="clear:both"}

**Table legend**: the first 3 columns contain the time complexity in the worst, average and best cases, column 4 the auxiliary space complexity, and column 5 the stability of the algorithm.

\\
**Note**: Stability means that 2 equal keys keep relative order after sorting (eg 5 4 4' 2 => 2 4 4' 5: 4' comes after 4 before and after sorting).

\\
Quick view:
{:style="clear:both"}
![pic_01](/assets/images/sort/sorting_1.png){:height="600pt"}

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

<pre>/ <a onclick="window.history.back()" style="cursor:pointer;"> Back </a> / <a href="/"> Home </a> / </pre>

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">