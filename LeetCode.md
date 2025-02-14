---
title: LeetCode Solutions
layout: default
---

# LeetCode Solutions

## Add Two Numbers

### Problem Description

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

#### Example 1:

**Input:** l1 = [2,4,3], l2 = [5,6,4]  
**Output:** [7,0,8]  
**Explanation:** 342 + 465 = 807.

#### Example 2:

**Input:** l1 = [0], l2 = [0]  
**Output:** [0]

#### Example 3:

**Input:** l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]  
**Output:** [8,9,9,9,0,0,0,1]

### Constraints:

- The number of nodes in each linked list is in the range [1, 100].
- 0 <= Node.val <= 9
- It is guaranteed that the list represents a number that does not have leading zeros.

---

### Solution

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int sum = l1->val + l2->val;
        int rem = sum / 10;
        ListNode* return_list = new ListNode(sum % 10);
        ListNode* l1_curr_node = l1->next;
        ListNode* l2_curr_node = l2->next;
        ListNode* new_curr_node = return_list;
        if (!l1_curr_node && !l2_curr_node && sum >= 10){
            new_curr_node->next= new ListNode(1);
        }
        while (l1_curr_node || l2_curr_node){
            sum = rem;
            if(l1_curr_node){
                sum += l1_curr_node->val;
                l1_curr_node = l1_curr_node->next;
            }
            if(l2_curr_node){
                sum += l2_curr_node->val;
                l2_curr_node = l2_curr_node->next;
            }
            new_curr_node->next= new ListNode(sum % 10);
            new_curr_node = new_curr_node->next;
            if (!l1_curr_node && !l2_curr_node && sum >= 10){
                new_curr_node->next= new ListNode(1);
            }
            rem = sum / 10;
        }
        return return_list;
    }
};
```
