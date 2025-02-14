<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Merge Sorted Array - LeetCode Solution</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 40px;
            background-color: #f8f9fa;
        }
        h1, h2, h3 {
            color: #343a40;
        }
        pre {
            background-color: #f4f4f4;
            padding: 10px;
            border-radius: 5px;
            overflow-x: auto;
        }
        .container {
            max-width: 800px;
            margin: auto;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        ul {
            padding-left: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Merge Sorted Array</h1>
        
        <h2>Problem Description</h2>
        <p>You are given two integer arrays <code>nums1</code> and <code>nums2</code>, sorted in non-decreasing order, and two integers <code>m</code> and <code>n</code>, representing the number of elements in <code>nums1</code> and <code>nums2</code> respectively.</p>
        <p>Merge <code>nums1</code> and <code>nums2</code> into a single array sorted in non-decreasing order.</p>
        
        <h3>Example 1:</h3>
        <p><strong>Input:</strong> nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3</p>
        <p><strong>Output:</strong> [1,2,2,3,5,6]</p>

        <h3>Example 2:</h3>
        <p><strong>Input:</strong> nums1 = [1], m = 1, nums2 = [], n = 0</p>
        <p><strong>Output:</strong> [1]</p>

        <h3>Example 3:</h3>
        <p><strong>Input:</strong> nums1 = [0], m = 0, nums2 = [1], n = 1</p>
        <p><strong>Output:</strong> [1]</p>

        <h2>Constraints:</h2>
        <ul>
            <li><code>nums1.length == m + n</code></li>
            <li><code>nums2.length == n</code></li>
            <li><code>0 <= m, n <= 200</code></li>
            <li><code>1 <= m + n <= 200</code></li>
            <li><code>-10^9 <= nums1[i], nums2[j] <= 10^9</code></li>
        </ul>

        <h2>Follow-up:</h2>
        <p>Can you come up with an algorithm that runs in <strong>O(m + n)</strong> time?</p>

        <h2>Solution</h2>
        <pre><code>
#include <vector>

class Solution {
public:
    void merge(std::vector<int>& nums1, int m, std::vector<int>& nums2, int n) {
        int i = m - 1;
        int j = n - 1;
        int k = m + n - 1;
        
        while (j >= 0) {
            if (i >= 0 && nums1[i] > nums2[j]) {
                nums1[k] = nums1[i];
                i--;
            } else {
                nums1[k] = nums2[j];
                j--;
            }
            k--;
        }
    }
};
        </code></pre>
    </div>
</body>
</html>
