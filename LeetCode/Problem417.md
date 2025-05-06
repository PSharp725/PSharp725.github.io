---
title: "LeetCode Problem 417: Pacific Atlantic Water Flow"
---

# Pacific Atlantic Water Flow

### Problem Description

There is an `m x n` rectangular island that borders both the **Pacific Ocean** and **Atlantic Ocean**.  
- The Pacific Ocean touches the island's **left and top edges**,  
- The Atlantic Ocean touches the island's **right and bottom edges**.

The island is partitioned into a grid of square cells. You are given an `m x n` integer matrix `heights` where `heights[r][c]` represents the height above sea level of the cell at coordinate `(r, c)`.

Rain water can flow:
- From a cell to its **north, south, east, or west** neighbor **if** the neighbor’s height is **less than or equal** to the current cell’s height.
- From any cell **adjacent to an ocean**, water can flow into that ocean.

**Return** a 2D list of coordinates `result` where `result[i] = [ri, ci]` means that rain water can flow from cell `(ri, ci)` to **both** the Pacific and Atlantic oceans.

---

---

### Example 1:

**Input:**

```
heights = {
  {1, 2, 2, 3, 5},
  {3, 2, 3, 4, 4},
  {2, 4, 5, 3, 1},
  {6, 7, 1, 4, 5},
  {5, 1, 1, 2, 4}
}
```

**Output:**

```
{
  {0, 4}, {1, 3}, {1, 4},
  {2, 2}, {3, 0}, {3, 1}, {4, 0}
}
```

**Explanation:**

These cells can reach both oceans:

- [0,4] → touches top (Pacific) and can flow right/down to Atlantic  
- [1,3] → via [0,3] to Pacific, and [1,4] to Atlantic  
- [2,2] → path to [0,2] for Pacific, and [2,3] → [2,4] for Atlantic  
- [3,0] → touches left edge (Pacific), path through [4,0] to Atlantic  
- [3,1] → path to [3,0] (Pacific), and [4,1] to Atlantic  
- [4,0] → on bottom-left, reaches both oceans directly

---

### Example 2:

**Input:**

heights = {
  {1}
}

**Output:**
```
{
  {0, 0}
}
```

**Explanation:**  
Single cell touches both Pacific and Atlantic.

---

### Constraints:

- `m == heights.length`
- `n == heights[r].length`
- `1 <= m, n <= 200`
- `0 <= heights[r][c] <= 10⁵`

---

### Solution

```cpp
class Solution {
public:
    void dfs(vector<vector<int>>& heights, vector<vector<bool>>& ocean, int i, int j) {
        int m = heights.size(), n = heights[0].size();
        ocean[i][j] = true;

        vector<pair<int, int>> directions = { {0,1},{1,0},{0,-1},{-1,0} };
        for (auto [dx, dy] : directions) {
            int x = i + dx;
            int y = j + dy;
            if (x >= 0 && x < m && y >= 0 && y < n &&
                !ocean[x][y] && heights[x][y] >= heights[i][j]) {
                dfs(heights, ocean, x, y);
            }
        }
    }
    vector<vector<int>> pacificAtlantic(vector<vector<int>>& heights) {
        int m = heights.size(), n = heights[0].size();
        vector<vector<bool>> pacific(m, vector<bool>(n, false));
        vector<vector<bool>> atlantic(m, vector<bool>(n, false));
        vector<vector<int>> result;

        for (int i = 0; i < m; ++i) {
            dfs(heights, pacific, i, 0);
            dfs(heights, atlantic, i, n - 1);
        }
        for (int j = 0; j < n; ++j) {
            dfs(heights, pacific, 0, j);
            dfs(heights, atlantic, m - 1, j);
        }

        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (pacific[i][j] && atlantic[i][j]) {
                    result.push_back({i, j});
                }
            }
        }

        return result;
    }
};
```