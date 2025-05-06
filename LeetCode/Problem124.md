---
title: "LeetCode Problem 124: Binary Tree Maximum Path Sum"
---

# Binary Tree Maximum Path Sum

### Problem Description

A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes is connected by an edge.  
- A node can appear **only once** in the sequence.  
- The path **does not** need to pass through the root.  
- The **path sum** is the sum of all node values in that path.

**Given the root of a binary tree**, return the **maximum path sum** among all possible non-empty paths.

---

### Example 1:

**Input:**

```
root = [1, 2, 3]
```

**Output:**

```
6
```

**Explanation:** The optimal path is 2 → 1 → 3 with sum = 2 + 1 + 3 = 6

---

### Example 2:

**Input:**

```
root = [-10, 9, 20, null, null, 15, 7]
```

**Output:** 

```
42
```

**Explanation:** The optimal path is 15 → 20 → 7 with sum = 15 + 20 + 7 = 42

---

### Constraints:

- The number of nodes in the tree is in the range [1, 30,000]  
- -1000 <= Node.val <= 1000

---

### Solution

```cpp
class Solution {
public:
    int maxGain(TreeNode* node, int& maxSum) {
        if (!node) return 0;

        // Only include positive gains
        int leftGain = max(maxGain(node->left, maxSum), 0);
        int rightGain = max(maxGain(node->right, maxSum), 0);

        // New path price includes current node
        int priceNewPath = node->val + leftGain + rightGain;

        // Update global max
        maxSum = max(maxSum, priceNewPath);

        // Return max gain from either side plus current node
        return node->val + max(leftGain, rightGain);
    }
    int maxPathSum(TreeNode* root) {
        int maxSum = INT_MIN;
        maxGain(root, maxSum);
        return maxSum;
    }
};
```