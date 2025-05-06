---
title: "LeetCode Problem 236: Lowest Common Ancestor of a Binary Tree"
---

# Lowest Common Ancestor of a Binary Tree

### Problem Description

Given a binary tree, find the **lowest common ancestor (LCA)** of two given nodes `p` and `q`.

According to the definition from Wikipedia:  
> "The lowest common ancestor is the lowest node in the tree that has both `p` and `q` as descendants (where we allow a node to be a descendant of itself)."

---

### Example 1:

**Input:**

```
root = [3, 5, 1, 6, 2, 0, 8, null, null, 7, 4]  
p = 5  
q = 1
```

**Output:** 

```
3
```

**Explanation:**  
The LCA of nodes 5 and 1 is 3.

---

### Example 2:

**Input:**

```
root = [3, 5, 1, 6, 2, 0, 8, null, null, 7, 4]  
p = 5  
q = 4
```

**Output:** 

```
5
```

**Explanation:**  
The LCA of nodes 5 and 4 is 5. A node can be its own descendant.

---

### Example 3:

**Input:**

```
root = [1, 2]  
p = 1  
q = 2
```

**Output:** 

```
1
```

---

### Constraints:

- The number of nodes is in the range [2, 10⁵]  
- -10⁹ <= Node.val <= 10⁹  
- All Node values are **unique**  
- `p != q`  
- Both `p` and `q` exist in the tree

---

### Solution

```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!root || root == p || root == q) return root;

        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);

        if (left && right) return root;
        return left ? left : right;
    }
};
```