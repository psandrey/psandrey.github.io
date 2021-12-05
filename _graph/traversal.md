---
layout: page
title: Graph Traversals
permalink: /traversal/
---

**Graph traversals** (or **graph search**) refers to the methods of visiting (and/or updating) the vertices of a graph. Depending on 
how the vertices are visited, we distinguish two methods: **breadth first search (BFS)** and **depth first search (DFS)**. In the former method, the neighbors are visited first, while in the latter are the children. 

\\
Let’s assume we are at some vertex $$ v $$.
If we follow **BFS** method, we visit all its immediate neighbours (i.e. paths with no intermediate vertices / direct edges), then we take these vertices one by one and visit all their immediate neighbours. We continue this way until all of them are visited. Funny thing, I call this the *plague* method, because the border between visited and unvisited vertices grows like a plague.
If we follow **DFS** method, then we visit one immediate neighbour of $$ v $$, and then continue with one immediate neighbour if this newly visited. Like for BFS, we continue this way until all vertices are visited. I call this the **snake** or the **digger** method, because we go as deeper as possible. DFS has the same profile as backtracking, because when there is nowhere to go deeper, we backtrack until we found some unvisited neighbour and again, we go deeper starting from this one. 
For better understanding, see the pictures below:
\\
**Breadth First Search (BFS):**\\
![pic_01](/graph/img/bfs_traversal_1.png){:height="600pt"}
\\
**Depth First Search (DFS):**\\
![pic_02](/graph/img/dfs_traversal_1.png){:height="600pt"}

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

  * <a href="/dfs/"> Depth-first search </a>
  * <a href="/bfs/"> Breadth-first search </a>
  * <a href="/cycle_topo/"> Cycle Detection / Topological Sort </a>

---