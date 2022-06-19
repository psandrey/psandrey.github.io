---
layout: page
title: All Pairs Shortest Paths
permalink: /graph/all_pairs_shortest_path/
---

The **Bellman-Ford** and **Dijkstra** algorithms find the single-source shortest-paths. Using the same idea, we can **generalize Bellman-Ford** and obtain all-pairs shortest paths in weighted digraph with no negative cycle. A better alternative is **Floyd–Warshall**, another dynamic programming algorithm which I like to call *the DP at its peak*. These two algorithms can be applied to weighted graphs with no-negative edges as well (just as Bellman-Ford). Another alternative to these DP algorithms is **Johnson's algorithm**. This one uses a combination of **Bellman-Ford** and **Dijkstra**. In short, it uses **Bellman-Ford** to make all weights positive and **Dijkstra** to find all-pairs shortest-paths.

\\
All-pairs Shortest-paths algorithms:
* <a href="/graph/all_pairs_shortest_path/generalized_bellman_ford/"> Generalization of Bellman-Ford </a>
* <a href="/graph/all_pairs_shortest_path/floyd_warshall/"> Floyd-Warshall </a>
* <a href="/graph/all_pairs_shortest_path/johnson/"> Johnson's algorithm </a>

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">
