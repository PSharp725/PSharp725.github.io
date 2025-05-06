---
title: "LeetCode Problem 329: Longest Increasing Path in a Matrix"
---

# Longest Increasing Path in a Matrix

### Problem Description

Given an `m x n` integer matrix, return the **length** of the longest increasing path in the matrix.

From each cell, you can move in **four directions**: up, down, left, or right. Diagonal movement and wrap-around are **not allowed**.

---

### Example 1:

**Input:**

```cpp
matrix = {
  {9, 9, 4},
  {6, 6, 8},
  {2, 1, 1}
};
```

**Output:** `4`

**Explanation:** The longest increasing path is `[1, 2, 6, 9]`

---

### Example 2:

**Input:**

```cpp
matrix = {
  {3, 4, 5},
  {3, 2, 6},
  {2, 2, 1}
};
```
**Output:** `4`


**Explanation:** The longest increasing path is `[3, 4, 5, 6]`. Diagonal movement is not allowed.

---

### Example 3:

**Input:**
```cpp
matrix = {
  {1}
};
```

**Output:** `1

---

### Constraints:

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 200`
- `0 <= matrix[i][j] <= 2³¹ - 1`

---

### Solution

```cpp
class Solution {
public:
    int dfs(vector<vector<int>>& matrix, vector<vector<int>>& memo, int i, int j) {
        if (memo[i][j] != 0) return memo[i][j];

        int m = matrix.size();
        int n = matrix[0].size();
        int maxLen = 1;
        vector<pair<int, int>> directions = {{0,1}, {1,0}, {0,-1}, {-1,0}};

        for (auto [dx, dy] : directions) {
            int x = i + dx;
            int y = j + dy;
            if (x >= 0 && x < m && y >= 0 && y < n && matrix[x][y] > matrix[i][j]) {
                maxLen = max(maxLen, 1 + dfs(matrix, memo, x, y));
            }
        }

        memo[i][j] = maxLen;
        return maxLen;
    }

    int longestIncreasingPath(vector<vector<int>>& matrix) {
        if (matrix.empty()) return 0;
        int m = matrix.size();
        int n = matrix[0].size();
        vector<vector<int>> memo(m, vector<int>(n, 0));
        int maxPath = 0;

        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                maxPath = max(maxPath, dfs(matrix, memo, i, j));
            }
        }
        return maxPath;
    }
};
```