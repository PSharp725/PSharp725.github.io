---
title: "LeetCode Problem 62: Unique Paths"
---

# Unique Paths

### Problem Description

There is a robot on an m x n grid. The robot is initially located at the top-left corner (i.e., `grid[0][0]`). The robot tries to move to the bottom-right corner (i.e., `grid[m - 1][n - 1]`). The robot can only move either down or right at any point in time.

Given the two integers `m` and `n`, return the number of possible unique paths that the robot can take to reach the bottom-right corner.

The test cases are generated so that the answer will be less than or equal to \(2 \times 10^9\).

#### Example 1:

**Input:** m = 3, n = 7  
**Output:** 28

#### Example 2:

**Input:** m = 3, n = 2  
**Output:** 3  
**Explanation:** From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down  
2. Down -> Down -> Right  
3. Down -> Right -> Down

### Constraints:

- \(1 \leq m, n \leq 100\)

---

### Solution

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        // Create a 2D vector to store the number of paths for each cell.
        vector<vector<int>> dp(m, vector<int>(n, 0));
        
        // Initialize the first row and first column.
        // There is only one way to reach any cell in the first row (all moves right)
        // and only one way to reach any cell in the first column (all moves down).
        for (int i = 0; i < m; i++) {
            dp[i][0] = 1;
        }
        for (int j = 0; j < n; j++) {
            dp[0][j] = 1;
        }
        
        // Fill in the rest of the table.
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }
        
        return dp[m-1][n-1];
    }
};
```
