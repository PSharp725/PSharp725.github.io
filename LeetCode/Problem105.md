---
title: "LeetCode Problem 105: Construct Binary Tree from Preorder and Inorder Traversal"
---

# Construct Binary Tree from Preorder and Inorder Traversal

### Problem Description

You are given two integer arrays `preorder` and `inorder` representing the preorder and inorder traversal of a binary tree.  
Construct and return the **binary tree**.

---

### Example 1:

**Input:**

```
preorder = [3, 9, 20, 15, 7]  
inorder = [9, 3, 15, 20, 7]
```

**Output:** 

```
[3, 9, 20, null, null, 15, 7]
```

---

### Example 2:

**Input:**

```
preorder = [-1]  
inorder = [-1]
```

**Output:** 

```
[-1]
```

---

### Constraints:

- 1 <= preorder.length <= 3000  
- `inorder.length == preorder.length`  
- -3000 <= preorder[i], inorder[i] <= 3000  
- All values in `preorder` and `inorder` are **unique**  
- `preorder` is guaranteed to be the preorder traversal of the tree  
- `inorder` is guaranteed to be the inorder traversal of the tree

---

### Solution

```cpp
class Solution {
public:
    TreeNode* build(vector<int>& preorder, int preStart, int preEnd,
                    vector<int>& inorder, int inStart, int inEnd,
                    unordered_map<int, int>& in_map) {
        if (preStart > preEnd || inStart > inEnd)
            return nullptr;

        int rootVal = preorder[preStart];
        TreeNode* root = new TreeNode(rootVal);
        int inRoot = in_map[rootVal];
        int numsLeft = inRoot - inStart;

        root->left = build(preorder, preStart + 1, preStart + numsLeft,
                           inorder, inStart, inRoot - 1, in_map);
        root->right = build(preorder, preStart + numsLeft + 1, preEnd,
                            inorder, inRoot + 1, inEnd, in_map);

        return root;
    }
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        unordered_map<int, int> in_map;
        for (int i = 0; i < inorder.size(); ++i) {
            in_map[inorder[i]] = i;
        }

        return build(preorder, 0, preorder.size() - 1,
                     inorder, 0, inorder.size() - 1,
                     in_map);
    }
};
```