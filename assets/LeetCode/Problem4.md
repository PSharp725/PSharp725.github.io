<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Find Median of Two Sorted Arrays - LeetCode Solution</title>
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
        <h1>Find Median of Two Sorted Arrays</h1>
        
        <h2>Problem Description</h2>
        <p>Given two sorted arrays <code>nums1</code> and <code>nums2</code> of size <code>m</code> and <code>n</code> respectively, return the median of the two sorted arrays.</p>
        <p>The overall run time complexity should be <strong>O(log (m+n))</strong>.</p>
        
        <h3>Example 1:</h3>
        <p><strong>Input:</strong> nums1 = [1,3], nums2 = [2]</p>
        <p><strong>Output:</strong> 2.00000</p>
        <p><strong>Explanation:</strong> merged array = [1,2,3] and median is 2.</p>

        <h3>Example 2:</h3>
        <p><strong>Input:</strong> nums1 = [1,2], nums2 = [3,4]</p>
        <p><strong>Output:</strong> 2.50000</p>
        <p><strong>Explanation:</strong> merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.</p>

        <h2>Constraints:</h2>
        <ul>
            <li><code>nums1.length == m</code></li>
            <li><code>nums2.length == n</code></li>
            <li><code>0 <= m <= 1000</code></li>
            <li><code>0 <= n <= 1000</code></li>
            <li><code>1 <= m + n <= 2000</code></li>
            <li><code>-10^6 <= nums1[i], nums2[i] <= 10^6</code></li>
        </ul>

        <h2>Solution</h2>
        <pre><code>
class Solution {
public:
    double findMedianSortedArrays(std::vector<int>& nums1, std::vector<int>& nums2) {
        int m = nums1.size();
        int n = nums2.size();
        int o = m + n;

        std::vector<int> num_tot = nums1;
        num_tot.insert(num_tot.end(), nums2.begin(), nums2.end());

        std::sort(num_tot.begin(), num_tot.end());

        if (o % 2 == 1) {
            return static_cast<double>(num_tot[o / 2]);
        } else {
            return (static_cast<double>(num_tot[o / 2]) + static_cast<double>(num_tot[(o / 2) - 1])) / 2.0;
        }
    }
};
        </code></pre>
    </div>
</body>
</html>
