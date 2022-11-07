---
layout: page
title: Heap Sort
permalink: /sort/comparison_sort/heap_sort/
---

* toc
{:toc}

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

<pre>/ <a onclick="window.history.back()" style="cursor:pointer;"> Back </a> / <a href="/"> Home </a> / </pre>

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

## Prerequisite

**Heap Definition**: A heap is a tree data structure that satisfies the max-heap or min-heap property, where:
- Max-heap property: any node of the tree has its value bigger than the values of its children; 
- Min-heap property: any node of the tree has its value smaller than the values of its children.
The most common implementation of this data structure is the binary-heap one. A binary-heap is represented as a full binary tree (i.e. a binary tree in which every level is completely filled, except perhaps the last one which is filled from left to right). Since a heap is a complete binary tree, it can easily be represented by an array. This way of representation is very efficient from the point of view of the space used.

### Array representation of binary-heaps

- $$ parent[i] = \left \lceil \frac{i}{2} \right \rceil- 1 $$.
- $$ left[i] = 2\cdot i + 1 $$.
- $$ right[i] = 2\cdot i + 2 $$.

{:style="clear:both"}
![pic_02](/assets/images/sort/comparison/heap_sort/comparison_sort_heap_sort_2.png){:height="180pt"}\\
![pic_01](/assets/images/sort/comparison/heap_sort/comparison_sort_heap_sort_1.png){:height="100pt"}

Heaps properties:
- **Max-heap property**: array[Parent(i)] >= array[i]
- **Min-heap property**: array[Parent(i)] <= array[i]

Common cases where binary heaps are used are priority queues and heapsort. Heapsort was proposed by J. W. J. Williams in 1964, in fact, J. W. J. Williams was the first to propose the heap data structure.

\\
The main operations required by heapsort are:
- Rise: restore the binary heap property for the rightmost item in the array (the farthest leaf);
- Sink: restore the binary heap property for the leftmost item in the array (the root);
- Build-Heap: re-arrange a sequence of items in a binary heap structure;

#### Sink

The *Sink* procedure restores the heap property for the leftmost element in the array (the first element – the root) if all other elements in the sequence satisfy the property. This is done by recursively sinking the element until the property is restored. Basically, sinking a node means exchanging it with the child that has the highest value (if it is max heap or the smallest if it is min heap). The element is swapped until both children have a smaller value (for max heap) or the element becomes a leaf, see example below.

{:style="clear:both"}
![pic_03](/assets/images/sort/comparison/heap_sort/comparison_sort_heap_sort_3.png){:height="300pt"}


**Sink implementation for max heap**:

```cpp
void sink(vector<int>& heap, int n, int i) {
    if (i >= n) return;

    int l = 2 * i + 1, r = 2 * i + 2;
    int hi = i;
    if (l < n && heap[hi] < heap[l]) hi = l;
    if (r < n && heap[hi] < heap[r]) hi = r;

    if (hi != i) {
        swap(heap[hi], heap[i]);
        sink(heap, n, hi);
    }
}
```

#### Rise

The *Rise* procedure restores the heap property for the rightmost element in the array (the last element – the outermost leaf) assuming that all other elements in the sequence satisfy the property. This is done by recursively rising the element until the property is restored. Basically, rising a node means changing it with the parent if the parent has a lower value (for max heap and a higher value for min heap). The element is swapped until its parent has a larger value (for max heap) or the element becomes the root, see example below.

{:style="clear:both"}
![pic_03](/assets/images/sort/comparison/heap_sort/comparison_sort_heap_sort_4.png){:height="280pt"}

**Rise implementation for max heap**:

```cpp
void rise(vector<int>& heap, int i) {
    if (i == 0) return;

    int p = (i - 1) / 2;
    if (heap[p] < heap[i]) {
        swap(heap[p], heap[i]);
        rise(heap, p);
    }
}
```

#### Build Max Heap

The heap can be built using sink or rise. If sink is used, then this procedure is called for all nodes starting with the penultimate level in the binary tree (since the leaves have nowhere to sink): $$ \frac{n}{2}, \frac{n}{2} -1. \frac{n}{2}-2, ... ,0 $$. If rise is used, then the procedure is called for all elements starting with the second level: $$ 1, 2, 3, ... ,n $$.

**Build max heap implementation**:

```cpp
void buildMaxHeap(vector<int>& a) {
    for (int i = 1; i < (int)a.size(); i++)
        rise(a, i);
}
```

#### Time Complexity

In the worst case, if the root violates the heap property then the Sink routine sinks it until the bottom of the tree. Since the tree is a complete binary tree then its height is $$ O(log_{2}n) $$, thus the asymptotic complexity is logarithmic. In the average-case the root is sunk only until the middle of the tree, thus the complexity is $$ O \left ( log_{2}\frac{n}{2} \right )= O(log_{2}n) $$, so still logarithmic.
The time complexity for the Rise is similar. If the rightmost item violates the property, then in the worst case the routine rises it until it becomes the root of the tree or until the middle of the tree in the average case. So, the complexity is still logarithmic: $$ O(log_{2}n) $$.

\\
Looking at the buildMaxHeap routine, the *Sink* routine is called n/2 times, hence it can be concluded that the time complexity for Build Max Heap is driven by the *Sink* routine. Since *Sink* has the time complexity of logarithmic nature in both worst case and average-case, the time complexity of Build Max Heap is: $$ O(nlog_{2}n) $$. However, according to CLRS, section 6.3 a tighter complexity was found based on the idea that the Sink varies with the tree height: $$ T(n) = O(n) $$ - I suggest to take a look to that proof.

## The Algorithm

Heapsort is a comparison-based sorting algorithm and can be seen as an improved Selection-Sort.

### Description
The main idea of Heapsort is to iteratively extract the element with the highest value from the unsorted sequence and move it to a sorted sequence using a heap structure. At each step in the iteration, the element with the largest value is found by maintaining a heap structure using the *Sink* routine. The algorithm can be summarized in the following three steps:
- **Step 1**: A heap structure is constructed by calling Build Max Heap, thus the item with the highest value is the root and all items in the sequence obey the max heap property;
- **Step 2**: The root (being the greatest) is exchanged with the last item in the heap (thus the new root violates the max heap property) and then the heap size is decreased by one excluding the old root (now moved to the tail) from the heap;
- **Step 3**: The max-heap property is restored by calling Sink for the new root.
*Steps 2 and 3 are repeated until the heap is diminished and becomes empty.*

### Implementation

```cpp
void sort(vector<int>& a) {
    buildMaxHeap(a);

    int n = (int)a.size();
    for (int i = n - 1; i >= 0; i--) {
        swap(a[0], a[i]);
        sink(a, i, 0);
    }
}

void buildMaxHeap(vector<int>& a) {
    for (int i = 1; i < (int)a.size(); i++)
        rise(a, i);
}

void rise(vector<int>& heap, int i) {
    if (i == 0) return;

    int p = (i - 1) / 2;
    if (heap[p] < heap[i]) {
        swap(heap[p], heap[i]);
        rise(heap, p);
    }
}

void sink(vector<int>& heap, int n, int i) {
    if (i >= n) return;

    int l = 2 * i + 1, r = 2 * i + 2;
    int hi = i;
    if (l < n && heap[hi] < heap[l]) hi = l;
    if (r < n && heap[hi] < heap[r]) hi = r;

    if (hi != i) {
        swap(heap[hi], heap[i]);
        sink(heap, n, hi);
    }
}
```

## Complexity Analysis

### Time Complexity

The time complexity in the worst and average cases are: $$ T(n) = T_{buildMaxHeap} + \sum (T_{sink} + O(1)) = O(n) + \sum (O(log_{2}n) + O(1)) = O(n) + O(nlog_{2}n) = O(nlog_{2}n) $$.

\\
**Note**: The complete and detailed analysis by Russel Schaffer and Robert Sedgewick can be found in the paper "The Analysis of Heapsort".

### Space Complexity (auxiliary)

There no auxiliary structure used, so $$ S(n) = O(1) $$.

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

<pre>/ <a onclick="window.history.back()" style="cursor:pointer;"> Back </a> / <a href="/"> Home </a> / </pre>

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">