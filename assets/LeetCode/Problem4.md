---
layout: default
title: "LeetCode Problem 4"
show_header: false
---


## Find Median of Two Sorted Arrays

### Problem Description

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return the median of the two sorted arrays.

The overall run time complexity should be **O(log (m+n))**.

#### Example 1:

**Input:** nums1 = [1,3], nums2 = [2]  
**Output:** 2.00000  
**Explanation:** merged array = [1,2,3] and median is 2.

#### Example 2:

**Input:** nums1 = [1,2], nums2 = [3,4]  
**Output:** 2.50000  
**Explanation:** merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.

### Constraints:

- `nums1.length == m`
- `nums2.length == n`
- `0 <= m <= 1000`
- `0 <= n <= 1000`
- `1 <= m + n <= 2000`
- `-10^6 <= nums1[i], nums2[i] <= 10^6`

---

### Solution

```cpp
class Solution {
public:
    double findMedianSortedArrays(std::vector<int>& nums1, std::vector<int>& nums2) {
        int m = nums1.size();
        int n = nums2.size();
        int o = m + n;

        // Merge the two vectors
        vector<int> num_tot = nums1;
        num_tot.insert(num_tot.end(), nums2.begin(), nums2.end());

        // Sort the merged vector
        sort(num_tot.begin(), num_tot.end());

        // Compute the median
        if (o % 2 == 1) {
            return static_cast<double>(num_tot[o / 2]);
        } else {
            return (static_cast<double>(num_tot[o / 2]) + static_cast<double>(num_tot[(o / 2) - 1])) / 2.0;
        }
    }
};
```

