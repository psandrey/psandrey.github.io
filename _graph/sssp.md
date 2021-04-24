---
layout: page
title: Single Source Shortest Path
permalink: /sssp/
---

The shortest-path problem is about finding the shortest distance between two vertices in a graph. If the graph is weighted, then the distance is defined as the sum of the weights that make it up or if it is not weighted then either we can consider that each edge has a weight of 1 and apply the same algorithms or define the distance as the number of the edges and look for a simpler algorithm.\\
So, now let's write some math and define these terms a little more rigorously.

\\
***Shortest path in unweighted graphs :*** Given an unweighted graph $$ G=(V,E) $$, the shortest path (or shortest dipath if G is directed) from vertex $$ v_i∈V $$ to $$ v_j∈V $$ is defined as any path $$ p=〈v_i,…,v_j〉 $$ with minimum number of edges:
* $$ {dist}_{min} (v_i,v_j )= min \left \{ length(p) = count(e\in p): v_i\overset{p}{\rightarrow}v_j \right \} $$, if  $$ ∃p⊆E $$
* $$ {dist}_{min} (v_i,v_j )= \infty $$, if $$ ∄p $$

\\
***Shortest path in weighted graphs :*** Given a weighted graph $$ G=(V,E) $$ and $$ w:E\rightarrow R $$ a weight function, the shortest path (or shortest dipath if G is directed) from vertex $$ v_i∈V $$ to $$ v_j∈V $$ is defined as any path $$ p=〈v_i,…,v_j〉 $$ with minimum weight:
* $$ {dist}_{min} (v_i,v_j )= min \left \{ w(p) = {\sum }_{(u,v)\in p)} w(u,v): v_i\overset{p}{\rightarrow}v_j \right \} $$, if $$ ∃p⊆E $$
* $$ {dist}_{min} (v_i,v_j )= \infty $$, if $$ ∄p $$

\\
Single Source Shortest Path algorithms:
* Weighted graph/digraph
  * <a href="/bellman_ford/"> Bellman-Ford </a>
  * <a href="/dijkstra/"> Dijkstra </a>
* Unweighted graph/digraph
  * Breadth-First Search

---
