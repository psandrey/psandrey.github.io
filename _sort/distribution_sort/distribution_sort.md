---
layout: page
title: Distribution Sorting Algorithms
permalink: /sort/distribution_sort/
---

Distribution Sorting is a class of algorithms that sorts a set of items in linear time, but the input data must satisfy some special constraints. In short, the items can be sorted faster than comparison-sort whenever the input data can be redistributed to intermediate bins and then collected in order and placed on output. Follow the links below for the following algorithms that falls in this class:  Counting sort, Radix sort, Pigeonhole Sort and Bucket sort. A short note: each of these algorithms imposes a different set of constraints to input data, thus each of them addresses a very narrow class of problems. \\

It is worth mentioning that on machines with multiple processing units these methods become really interesting because the intermediary bins can be placed on different units and sorted in parallel, thus the time complexity is improved considerably.


 <hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

  * <a href="/sort/distribution_counting_sort/"> Counting Sort </a>
  * <a href="/sort/distribution_radix_sort/"> Radix Sort </a>
  * <a href="/sort/distribution_pigeonhole_sort/"> Pigeonhole Sort </a>
  * <a href="/sort/distribution_bucket_sort/"> Bucket Sort </a>

---