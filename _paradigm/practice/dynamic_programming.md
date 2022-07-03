---
layout: page
title: Practice Dynamic Programming
permalink: /paradigm/practice/dynamic_programming
---

* toc
{:toc}

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

<pre>/ <a onclick="window.history.back()" style="cursor:pointer;"> Back </a> / <a href="/"> Home </a> / </pre>

<hr style="height:1px; border:none; color:#ccc; background-color:#ccc;">

## Prefixes/Suffixes

### Kadane's Algorithm

TODO

### Largest Sum Contiguous Subarray

Write an efficient program to find the sum of contiguous subarray within a one-dimensional array of numbers which has the largest sum.

```cpp
// memoization
int LSCS_memo(vector<int>& a) {
    int ans = INT_MIN;

    vector<int> memo(a.size(), -1);
    ans = 0;
    for (int n = 0; n < (int)a.size(); n++)
        ans = max(ans, LSCS_memo_helper(a, n, memo));

    return ans;
}

int LSCS_memo_helper(vector<int>& a, int i, vector<int>& memo) {
    if (i == 0) return 1;
    if (memo[i] != -1) return memo[i];

    int ans_prev = LSCS_memo_helper(a, i - 1, memo);
    int ans = a[i];
    if (ans_prev > 0) ans += ans_prev;

    memo[i] = ans;
    return memo[i];
}

// tabulation
int LSCS_tab(vector<int>& a) {
    vector<int> dp(a.size());

    int max_end_here = a[0], max_so_far = a[0];
    for (int i = 1; i < (int)a.size(); i++) {
        max_end_here = max(a[i], max_end_here + a[i]);
        max_so_far = max(max_so_far, max_end_here);
    }

    return max_so_far;
}
```

## Interval

### Longest Common Subsequence

TODO

### Edit Distance (Levenshtein distance)

TODO

## Bitmask

### Bellman-Held-Karp (Shortest Superstring Problem)

TODO

## Pseudo-polynomial

### Rod cutting

Suppose you have a rod of length $$ n $$, and you want to cut up the rod and sell the pieces in a way that maximizes the total amount of money you get. A piece of length $$ i $$ is worth $$ p_i $$ dollars.

```cpp
// memoization
int rod_cut(vector<int>& p) {
    int ans = 0;

    vector<int> memo(p.size(), -1);
    ans = rod_cut_memo(p, p.size(), memo);

    return ans;
}

int rod_cut_memo(vector<int>& p, int len, vector<int>& memo) {
    if (len == 0) return 0;
    if (memo[len-1] != -1) return memo[len];

    int ans = INT_MIN;
    for (int i = 0; i < len; i++) {
        int cur = p[i] + rod_cut_memo(p, len - i - 1);
        ans = max(ans, cur);
    }

    memo[len-1] = ans;
    return memo[len-1];
}

// tabulation
int rod_cut_tab(vector<int>& p) {
    vector<int> dp(p.size()+1);

    dp[0] = 0;
    for (int i = 1; i <= (int)p.size(); i++) {
        dp[i] = INT_MIN;
        for (int j = 1; j <= i; j++)
            dp[i] = max(dp[i], dp[i - j] + p[j-1]);
    }

    return dp[p.size()];
}
```

### Knapsack 0-1

Given weights and values of n items, put these items in a knapsack of capacity W to get the maximum total value in the knapsack. In other words, given two integer arrays val[0..n-1] and wt[0..n-1] which represent values and weights associated with n items respectively. Also given an integer W which represents knapsack capacity, find out the maximum value subset of val[] such that sum of the weights of this subset is smaller than or equal to W. You cannot break an item, either pick the complete item, or don’t pick it (0-1 property).

```cpp
// memoization
int knap_memo(vector<int>& w, vector<int>& p, int cap) {
    int ans = 0;
    int n = (int)w.size();

    vector<vector<int>> memo(cap + 1, vector<int>(n + 1, -1));
    ans = knap_memo(w, p, n, cap, memo);

    return ans;
}

int knap_memo_helper(vector<int>& w, vector<int>& p, int k, int cap, vector<vector<int>>& memo) {
    if (memo[cap][k] != -1)	return memo[cap][k];
    if (cap == 0 || k == 0) memo[cap][k] = 0;
    else {
        int take = 0;
        int notake = knap_memo_helper(w, p, k - 1, cap, memo);
        if (w[k - 1] <= cap) take = knap_memo_helper(w, p, k - 1, cap - w[k - 1], memo) + p[k - 1];

        memo[cap][k] = max(take, notake);
    }
    return memo[cap][k];
}

// tabulation
int knap_tab(vector<int>& w, vector<int>& p, int W) {
    int n = (int)w.size();

    vector<vector<int>> dp(W + 1, vector<int>(2, 0));

    int j = 0;
    for (int k = 1; k <= n; k++) {
        j ^= 1;
        for (int cap = 0; cap <= W; cap++) {
            if (w[k - 1] > cap) dp[cap][j ^ 1] = dp[cap][j ^ 1];
            else dp[cap][j] = max(dp[cap][j ^ 1], dp[cap - w[k - 1]][j ^ 1] + p[k - 1]);
        }
    }

    return dp[W][j];
}
```

### Coin Change Problem

Given a value S, and an infinite supply of c = { c1, c2, .. , cn} valued coins:
1. In how many ways we can pay the value S with the given coins?
2. What is the minimum number of coins we need to pay value S? 

#### Question 1
```cpp
// memoization
int coins_ways(vector<int>& c, int S) {
    int ans = 0;
    if (c.size() == 0) return ans;

    int n = (int)c.size();
    vector<vector<int>> memo(S + 1);
    for (int i = 0; i <= S; i++) memo[i] = vector<int>(n, -1);

    ans = coins_ways_memo(c, 0, S, memo);

    return ans;
}

int coins_ways_memo(vector<int>& c, int i, int S, vector<vector<int>>& memo) {
    if (S == 0)
        return 1;
    if (i == (int)c.size()) return 0;
    if (memo[S][i] != -1) return memo[S][i];

    int take = 0, notake = 0;
    if (S >= c[i]) take = coins_ways_memo(c, i, S - c[i], memo);
    notake = coins_ways_memo(c, i + 1, S, memo);

    memo[S][i] = take + notake;
    return memo[S][i];
}

// tabulation
int coins_ways_tab(vector<int>& c, int S) {
    int n = (int)c.size();
    vector<vector<int>> dp(S + 1);
    for (int i = 0; i <= S; i++) dp[i] = vector<int>(n + 1, 0);
    for (int i = 0; i <= n; i++) dp[0][i] = 1;

    for (int s = 1; s <= S; s++)
        for (int i = 1; i <= n; i++) {
            dp[s][i] = dp[s][i - 1];
            if (s >= c[i - 1]) dp[s][i] += dp[s - c[i - 1]][i];
        }

    return dp[S][n];
}

int coins_ways_tab_pile(vector<int>& c, int S) {
    int n = (int)c.size();
    vector<int> dp(S + 1, 0);
    dp[0] = 1;
    for (int i = 0; i < n; i++)
        for (int s = 1; s <= S; s++)
            if (s >= c[i]) dp[s] = dp[s] + dp[s - c[i]];

    return dp[S];
}

```

#### Question 2

```cpp
// memoization
int coins_min_memo(vector<int>& c, int S, vector<int>& memo) {
    if (S == 0) return 0;
    if (memo[S] != -1) return memo[S];

    int ans = INT_MAX;
    int n = (int)c.size();
    for (int i = 0; i < n; i++) {
        int ans_i = INT_MAX;
        if (c[i] <= S) ans_i = coins_min_memo(c, S - c[i], memo);
        ans = (ans_i == INT_MAX ? ans : min(ans, ans_i + 1));
    }

    memo[S] = ans;
    return ans;
	}

// tabulation
int coins_min_tab(vector<int>& c, int S) {
    int n = (int)c.size();
    vector<int> dp(S + 1, S + 1);
    
    dp[0] = 0;
    for (int s = 1; s <= S; s++) {
        for (int j = 0; j < n; j++) {
            if (s >= c[j]) dp[s] = min(dp[s], dp[s - c[j]] + 1);
        }
    }

    return (dp[S] > S ? -1 : dp[S]);
}
```

---