---
layout: page
title: Algorithmic paradigm
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
| _2_ |     |     | Q   |     |     |     |     |     |
| _3_ | Q   |     |     |     |     |     |     |     |
| _4_ | X   | X   | X   | Q   |     |     |     |     |

\\
So, we have a queen on the third column on the first row and a queen on the first column on the second row. When we try to place the third queen on the third row, we prune the branches that are generated for first, second and third column since it attacks the previous placed queens. We can see that these positions are generated incrementally, and no possible position is omitted. The forth position is valid, so we place the queen there and then we try the next queen on the next row.

{:style="clear:both"}

\\
So, we can deduce two important properties for the Backtracking paradigm:
1. No repetition and completion: it is a generation method that avoids repetitions without omitting any solution;
2. Search pruning: because the final solutions are built incrementally, the partial solutions can be evaluated and the branches that are not leading to a valid final solution or lead to a worse that already known solution are pruned.

\\
Now, lets see a simple implementation for the 8-queens problem that returns the number of solutions:
1. Data structure to represent the state: a vector as a stack where the index in the vector represents the row and the value the current valid position for the queen on that row (basically, the column).
2. Check for valid position: two queens ca attack each other if they are on the same row, col or diagonal 
    * row attack: $$ row_{current} = row $$.
    * col attack: $$ col_{current} = col $$.
    * diagonal attack: $$ \left\| row_{current} - row \right\| = \left\| col_{current} - col \right\| $$ .
3. Check for solution: stack/vector size is equal to 8 – it means that we placed all queens on the table and any two pairs are not attacking each other.


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

	return true; // no attack, then the position is valid
}

```

### Practice Backtraking

Usually, we see problems in form of combinations or permutations and we need to enumerate all solutions that are within given constraints conditions. See below a few iconic problems to practice this paradigm:

1.	Generate permutations [leetcode](https://leetcode.com/problems/permutations/)
2.	Generate combinations [leetcode](https://leetcode.com/problems/combinations/)
3.	Generate all subsets of a given set [leetcode](https://leetcode.com/problems/subsets/)
4.	Generate all Parentheses [leetcode](https://leetcode.com/problems/generate-parentheses/)
5.	N-queens problem [leetcode](https://leetcode.com/problems/n-queens/)
6.	Sudoku [leetcode](https://leetcode.com/problems/sudoku-solver/)
7.	Palindrome partitioning [leetcode](https://leetcode.com/problems/palindrome-partitioning/)

## Divide and conquer

TODO

## Dynamic programming

TODO

## Greedy

TODO