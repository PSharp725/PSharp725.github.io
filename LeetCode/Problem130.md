---
title: "LeetCode Problem 130: Surrounded Regions"
---

# Surrounded Regions

### Problem Description

You are given an `m x n` matrix `board` containing letters `'X'` and `'O'`. You must capture all regions that are surrounded.

A **region** is formed by connecting adjacent `'O'` cells horizontally or vertically. A region is **surrounded** if it is entirely enclosed by `'X'` cells and **none** of its `'O'` cells are on the border of the board.

To capture a region, replace all `'O'`s in that region with `'X'`s — **in-place**. No value is returned.

### Example 1:

**Input:**

```
board = [
["X","X","X","X"],
["X","O","O","X"],
["X","X","O","X"],
["X","O","X","X"]
]
```


**Output:**


```
[
["X","X","X","X"],
["X","X","X","X"],
["X","X","X","X"],
["X","O","X","X"]
]
```

**Explanation:** The bottom region is connected to the border, so it is not captured. The middle region is fully enclosed and is replaced.

### Example 2:

**Input:** `board = [["X"]]`  
**Output:** ` [["X"]]`

### Constraints:

- `m == board.length`
- `n == board[i].length`
- `1 <= m, n <= 200`
- `board[i][j]` is `'X'` or `'O'`

---

### Solution

```cpp
class Solution {
public:
    void dfs(vector<vector<char>>& board, int i, int j) {
        int m = board.size();
        int n = board[0].size();
        if (i < 0 || i >= m || j < 0 || j >= n || board[i][j] != 'O')
            return;

        board[i][j] = '#';  // mark safe

        dfs(board, i + 1, j);
        dfs(board, i - 1, j);
        dfs(board, i, j + 1);
        dfs(board, i, j - 1);
    }

    void solve(vector<vector<char>>& board) {
        int m = board.size();
        if (m == 0) return;
        int n = board[0].size();

        // Mark all 'O's on the edge and their connected 'O's
        for (int i = 0; i < m; ++i) {
            dfs(board, i, 0);
            dfs(board, i, n - 1);
        }
        for (int j = 0; j < n; ++j) {
            dfs(board, 0, j);
            dfs(board, m - 1, j);
        }

        // Flip captured regions
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (board[i][j] == 'O')
                    board[i][j] = 'X';  // captured
                else if (board[i][j] == '#')
                    board[i][j] = 'O';  // restore safe
            }
        }
    }
};
```