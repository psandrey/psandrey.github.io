---
layout: page
title: Algorithmic paradigms
permalink: /paradigm/
---

* toc
{:toc}

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

<pre>/ <a onclick="window.history.back()" style="cursor:pointer;"> Back </a> / <a href="/"> Home </a> / </pre>

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

## Brute-force search & Backtraking

You may ask why I put brute-force and backtracking in the same bucket... well, I've seen backtracking being referred as brute-force many times, simply because they have the same time-complexity in the worst-case. Even so, in practice backtracking is performing much better.\\
\\
The **Brute-force search** (aka. exhaustive search, generate-and-test) is an algorithmic paradigm that generates all possible candidates for the solutions and checks whether it satisfy the problem’s requirements.\\
\\
The **Backtracking** is an algorithmic paradigm that generates candidates for the solutions incrementally and discards them ("backtracks") if fail to satisfy the constraints of the problem and cannot possibly be completed to a solution. \\
\\
So, let’s consider the **eight queens puzzle**:  how to place 8 queens on an 8×8 chessboard such that none of them attack one another. \\
**Brute-force** means that we generate all possible arrangement of all these 8 queens on the chess board. So, the first queen on the first row has 8 possible positions, the second queen on the second row has another 8 possible positions… we place all 8 queens like this. So, there are $$ 8^8 $$ possibilities. After we placed all 8 queens and have generated a candidate, we check to see if that arrangement is a solution or not (basically, we check all pairs of queens to see if they atack each other). \\
**Backtracking** means that after we put the first queen on the first row on the board, we try to put the next queen on the second row, but we do not consider the positions where the second queen attacks the first one, therefore some branches are discarded. When we try to place the third queen on the third row, we omit the positions where it attacks the first and second queen, therefore some other branches are discarded. I think by now you got the picture of why backtracking performs better while both have the same time complexity in the worst-case.\\
\\
I will not spend time with brute-force, because is just a way to generate the permutations and sweep the entire search space, but backtracking deserves more attention. As a small note, in graph realm the Depth-First search is a specific form of backtracking, so we can "prepare the ground" for later :)
 
###  Backtracking

First let’s see some pseudocode for the recursive version of Backtracking:

```cpp
void backtracking(state, cnt) {
	if (solution(state) == true) {
		display(state);
		
	} else {	
		for (value = first to last) {
			if (valid(value) == false) continue;
			
			apply(state, value);
			backtracking(state);
			remove(state, value);
		}
	}
}
```

\\
In short, the code says:
* Is the current state a solution ? if yes, then display it
* If the current state is not a solution, then
    * if the current state is a leaf, then backtrack (return to the previous state)
    * if the current state is not a leaf, then add all valid values one by one to the state that can be generated incrementally and for each new valid state go to step 1.

Now, lets apply these steps to the 8-queens problem:
* Did we placed all 8 queens on the table ? if yes, then display table with the queens and then backtrack (basically, try the next valid position for the last queen, if any).
* If we still have queens to place on the table, then:
    * If there is no valid position to place the current queen, then backtrack (return to the previous queen and try to another position for it).
    * Otherwise, for all valid positions for the current queen, place it on each one and then try to place the next queen on the table (go to step 1).

To clear any doubts, lets see a picture of how to place the third queen on the third row:

{:style="float: left"}

| c\r | _1_ | _2_ | _3_ | _4_ | _5_ | _6_ | _7_ | _8_ |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| _1_ |     |     | Q   |     |     |     |     |     |
| _2_ | Q   |     |     |     |     |     |     |     |
| _3_ | X   | X   | X   | Q   |     |     |     |     |

\\
So, we have a queen on the third column on the first row and a queen on the first column on the second row. When we try to place the third queen on the third row, we prune the branches that are generated for first, second and third column since it attacks the previous placed queens. We can see that these positions are generated incrementally, and no possible position is omitted. The forth position is valid, so we place the queen there and then we try the next queen on the next row.

{:style="clear:both"}

\\
We can deduce two important properties for the Backtracking paradigm:
1. No repetition and completion: it is a generation method that avoids repetitions without omitting any solution;
2. Search pruning: because the final solutions are built incrementally, the partial solutions can be evaluated and the branches that are not leading to a valid final solution or lead to a worse that already known solution are pruned.

\\
Now, lets see a simple implementation for the 8-queens problem that returns the number of solutions:
1. The data structure used to represent the states: a vector used as a stack where the index in the vector represents the row and the value represents the current valid position for the queen on that row (basically, the column).
2. How to check if a position is valid: two queens are attacking each other if they are on the same row, col or diagonal 
    * row attack: $$ row_{current} = row $$.
    * col attack: $$ col_{current} = col $$.
    * diagonal attack: $$ \left\| row_{current} - row \right\| = \left\| col_{current} - col \right\| $$ .
3. How to check if the current state is a valid solution: the stack/vector size is equal to 8 – it means that we put all the queens on the table and any two pairs of queens don't attack each other.


```cpp
int queens(int n) {
	vector<int> st;
	return backtracking(st, n);
}

int backtracking(vector<int>& st, int n) {
	if (st.size() == n) return 1; // solution = all n queens placed on the table

	int w = 0;
	for (int j = 0; j < n; j++) {
		if (valid(st, j) == true) { // position is valid if current queen doesn't attack any previous placed queen
			st.push_back(j); // add position to the state
			w += backtracking(st, n); // try to place the next queen
			st.pop_back(); // remove the queen from the current position to try the next valid position
		}
	}

	return w; // returns the number of solutions for the current state
}

bool valid(vector<int>& st, int col) {
	int row = st.size();

	for (int i = 0; i < (int)st.size(); i++) {
		int j = st[i];
		if (i == row || j == col // check row and col
            || abs(col - j) == abs(row - i)) // check diagonals
			return false; // if attach on row, col or diagonal, then position is not valid
	}

	return true; // no attack so, the position is valid
}

```

### Iterative version

TODO

### Practice Backtraking

Usually, the problems that are solved by the backtracking method are in the form of combinations or permutations, and the requirement is to list all the solutions that satisfy some given constraints. See below some iconic problems you can use to practice this paradigm:

1.	Generate permutations [leetcode](https://leetcode.com/problems/permutations/)
2.	Generate combinations [leetcode](https://leetcode.com/problems/combinations/)
3.	Generate all subsets of a given set [leetcode](https://leetcode.com/problems/subsets/)
4.	Generate all Parentheses [leetcode](https://leetcode.com/problems/generate-parentheses/)
5.	N-queens problem [leetcode](https://leetcode.com/problems/n-queens/)
6.	Sudoku [leetcode](https://leetcode.com/problems/sudoku-solver/)
7.	Palindrome partitioning [leetcode](https://leetcode.com/problems/palindrome-partitioning/)

## Divide and conquer

**Divide and conquer** is an algorithmic paradigm that breaks a complex problem into smaller and  more easily solvable problems. Here are few important algorithms that uses this technique: mergesort, quicksort and performing matrix multiplication. One small note, binary search does not use divide and conquer technique – a divide and conquer algorithm have at least two **disjoint** recursive call which binary search does not have. \\
\\
So, a divide and conquer algorithm break down the initial problem (the general case) into two or more subproblems of the same type until it becomes simple enough to be solvable immediately (the base case). Then the solutions to these subproblems are combined to solve the original problem:
* Step 1 – **Divide** the given problem into a set of subproblems.
* Step 2 – **Conquer**: solve these subproblems recursively.
* Step 3 – **Combine** the solutions to the subproblems to solve the original problem.
Note: when you design an algorithm by using this technique, you need to define 2 things:
1.	The recursive formula (the general case)
2.	The stopping condition (the base case): the basic problem that can be solved immediately.

\\
**Note**: There is a strong relation between recurrences and Divide-and-conquer method for designing algorithms, please see
Asymptotic Analysis for Recurrences, The “Master Theorem” Method and The “Guess-and-Confirm” Method.

### Practice Divide and conquer

1. <a href="/sort/comparison_sort/merge_sort/"> Merge Sort </a>
2. <a href="/sort/comparison_sort/quick_sort/"> Quicksort </a>
3. Strassen's algorithm for matrix multiplication: [topcoder.com](https://www.topcoder.com/thrive/articles/strassenss-algorithm-for-matrix-multiplication)
4. Towers of Hanoi: [Briliant.org](https://brilliant.org/wiki/recurrence-relations-method-of-summation-factors/#example-1-the-tower-of-hanoi-problem)
5. Majority Element: [leetcode](https://leetcode.com/problems/majority-element/solution/)
6. Median of Two Sorted Arrays: [leetcode](https://leetcode.com/problems/median-of-two-sorted-arrays/)

## Dynamic programming

**Dynamic programming (DP)** is basically an optimization method over plain recursion. It was invented by Bellman in 1950. Bellman used this technique to solve the single-source shortest-path problem in a graph. As with divide and conquer, it is based on dividing the problem into subproblems which are solved recursively. The difference stays in the fact that the subproblems in divide and conquer are disjunctive (i.e. the subproblems are unique on every branch), while for DP some subproblems are overlapping. Thus, to avoid the redundant work we can cache the result of every subproblem when first solved so it can be reused when needed instead of recomputing – sacrifice some space  to speed up the algorithm. \\
\\
Storing/caching results can be done in two ways:
* memoization: store the results within the recursive calls
* tabulation: build a cache table iteratively from smallest subproblems to bigger subproblems

Both approaches can be applied to any problem that is solvable using DP and most of the time both approaches have the same time complexity, however in practice usualy the tabulation performs better, because it consumes less memory. TODO: give examples.

\\
I want to make a small note here, because I’ve seen that tabulation is referred as bottom-up approach and memoization as top-down approach. This is a common mistake; the DP is a bottom-up approach for both. For memoization recursion goes as deep as possible until the smallest problem is solved immediately (the base case) and on the way back the results are combined to solve the bigger subproblems, so it is a bottom-up approach. For tabulation is obvious... you need to fill the table from smaller to bigger problems.

\\
To be able to apply this technique, the problem must exhibit two properties:
* **Optimal structure**: if an optimal solution of a given problem can be obtain by using optimal solutions of its subproblems, then the problem exhibits the optimal structure property.
*  **Overlapping subproblems**: if a recursive algorithm visits the same subproblem more than once, then the problem exhibits the overlapping subproblems property.

\\
Assuming we have a problem thats has these properties, we can approach it in 5-6 steps (from [Erik Demaine](https://en.wikipedia.org/wiki/Erik_Demaine)’s lecture):
1. Define the subproblems. At this step you need to define how to represent subproblems and find the number of them (usually, we want a polynomial number). 
2. Relate subproblem's solutions recursively. At this step you need to define a recurrence over an acyclic graph (DAG). Basically, all subproblems dependency must for a DAG. 
3. Define the base case of the recurrence. If you use tabulation usually you need to prefill it with base cases or if you use memoization you need to define it and stop the recursive calls.
4. Build the algorithm by using memoization or tabulation.
5. Solve the original problem. Usually, the original problem is on of the subproblems or the larger one, but sometimes you need to combine some subproblems to solve the original one.
6. Time and space complexity analysis.

**Note:** I suggest to watch Erik's lectures, they are very good:
* [Dynamic Programming, Part 1: SRTBOT, Fib, DAGs, Bowling](https://www.youtube.com/watch?v=r4-cftqTcdI)
* [Dynamic Programming, Part 2: LCS, LIS, Coins](https://www.youtube.com/watch?v=KLBCUx1is2c)
* [Dynamic Programming, Part 3: APSP, Parens, Piano](https://www.youtube.com/watch?v=TDo3r5M1LNo)
* [Dynamic Programming, Part 4: Rods, Subset Sum, Pseudopolynomial](https://www.youtube.com/watch?v=i9OAOk0CUQE)

\\
DP problems are nice, because they also require some imagination, so you don't just have to apply a pattern to solve them. However, there is a classification/taxonomy that we can imagine depending on how we define the state at a given time:
* **Prefixes/Suffixes:** you must first solve the smaller subproblems from beginning (or end) and expand subproblems towards the end (or the beginning). Examples: Kadane’s algorithm for Largest Sum Contiguous Subarray, Largest Increasing Subsequence.
* **Interval:** you must first solve the small subproblems for each index and then extend the subproblem size to the size of the initial problem for the $$ 0 $$ index. Examples: Longest Common Subsequence, Edit Distance (Levenshtein distance), Matrix Chain Ordering, Bellman-Ford, Floyd-Warshall.
* **Bitmask (*intractable problems*):** the subproblems are divided in subsets and you must first solve the smaller subsets and expand up to the entire set. Example: Bellman-Held-Karp – Shortest Superstring Problem.
* **Pseudo-polynomial:** you must first solve the smaller subproblems in size and expand up to the maximum numeric value of the input (the largest integer in the input not the length of the input). Examples: Rod cutting, Knapsack 0-1, Coin Change Problem, Partition Problem. 

### Practice Dynamic Programming

* Prefixes/Suffixes: 
	1. TODO: Kadane
	2. TODO: Largest Sum Contiguous Subarray
	3. Largest Increasing Subsequence: [topcoder.com](https://www.topcoder.com/thrive/articles/longest-increasing-subsequence?utm_source=thrive&utm_campaign=thrive-feed&utm_medium=rss-feed)
* Interval:
	1. TODO: Longest Common Subsequence
	2. TODO: Edit Distance (Levenshtein distance)
	3. <a href="/graph/single_source_shortest_path/bellman_ford/"> Bellman-Ford </a>
	4. <a href="/graph/all_pairs_shortest_path/floyd_warshall/"> Floyd-Warshall </a>
* Bitmask:
	1. TODO: Bellman-Held-Karp (Shortest Superstring Problem)
* Pseudo-polynomial:
	1. TODO: Rod cutting
	2. TODO: Knapsack 0-1
	3. TODO: Coin Change Problem

## Greedy

A **greedy** algorithm is a heuristic algorithm of making local optimal choice with the hope to obtain global optimum. Basically, it makes a greedy choice at each step, and it never goes back to change its choice. \\
\\
**Note:** Most greedy algorithms are not correct, however sometimes is close enough to the optimal solution. \\
\\
A greedy algorithm is correct if it exhibits the following two properties:
* **Optimal structure**: if an optimal solution of a given problem can be obtain by using optimal solutions of its subproblems (just like DP).
* **Greedy choice property**: a global optimum can be obtained by making the optimal local choice.

**Note:** Usually, a greedy algorithm is easy to find, and it is easy to analyse its complexity, but it is hard to prove is correctness (most of the times it involves some imagination rather than math skills).

\\
When you need to approach a greedy problem, you can follow the following three steps:
1.	First, check if it is feasible.
2.	Define the local optimum choice.
3.	The choice must be unalterable: once the decision is made at any subsequent step the option does not need to be changed.

### Practice Greedy

1. <a href="/graph/single_source_shortest_path/dijkstra/"> Single-Source Shortest Paths — Dijkstra’s Algorithm </a>
2. <a href="/graph/minimum_spanning_tree/kruskal/"> Kruskal’s Algorithm for finding Minimum Spanning Tree </a>
3. <a href="/graph/minimum_spanning_tree/prim/"> Prim’s Algorithm for finding Minimum Spanning Tree </a>
4. Graph Coloring Problem [brilliant.org](https://brilliant.org/wiki/graph-coloring-and-chromatic-numbers/)
5. Gas Station [leetcode](https://leetcode.com/problems/gas-station/)
6. Jump Game [leetcode](https://leetcode.com/problems/jump-game/)
7. Container With Most Water [leetcode](https://leetcode.com/problems/container-with-most-water/)

## More reading

* Backtracking
    * [Briliant.org](https://brilliant.org/wiki/recursive-backtracking/)
    * Skiena, second edition, section 7.1, pg. 231
* Divide and conquer
    * [Briliant.org](https://brilliant.org/wiki/divide-and-conquer/)
    * Skiena, second edition, section 4.10, pg. 135
	* Cormen, third edition, section 4, pg. 65
* Dynamic Programming
    * Erik's lectures
        * [Dynamic Programming, Part 1: SRTBOT, Fib, DAGs, Bowling](https://www.youtube.com/watch?v=r4-cftqTcdI)
        * [Dynamic Programming, Part 2: LCS, LIS, Coins](https://www.youtube.com/watch?v=KLBCUx1is2c)
        * [Dynamic Programming, Part 3: APSP, Parens, Piano](https://www.youtube.com/watch?v=TDo3r5M1LNo)
        * [Dynamic Programming, Part 4: Rods, Subset Sum, Pseudopolynomial](https://www.youtube.com/watch?v=i9OAOk0CUQE)
	* Skiena, second edition, section 8, pg. 274
	* [Topcoder.com](https://www.topcoder.com/thrive/articles/Dynamic%20Programming:%20From%20Novice%20to%20Advanced)
	* [Briliant.org](https://brilliant.org/wiki/problem-solving-dynamic-programming/?subtopic=algorithms&chapter=dynamic-programming)
* Greedy
    * [Briliant.org](https://brilliant.org/wiki/greedy-algorithm/)
	* [topcoder.com](https://www.topcoder.com/thrive/articles/Greedy is Good)

---