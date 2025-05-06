---
title: "LeetCode Problem 218: The Skyline Problem"
---

# The Skyline Problem

### Problem Description

A city's skyline is the outer contour of the silhouette formed by all the buildings in that city when viewed from a distance. Given the positions and heights of all the buildings, return the skyline formed by these buildings.

Each building is represented as a triplet `[lefti, righti, heighti]` where:
- `lefti` is the x-coordinate of the left edge,
- `righti` is the x-coordinate of the right edge,
- `heighti` is the height of the building.

All buildings are **perfect rectangles** resting on a flat surface (height 0).

The **skyline** should be returned as a list of key points in the format `[[x1,y1], [x2,y2], ...]`.  
Each key point represents a critical change in height. The last point in the list must have `y=0` to indicate the end of the skyline.

Note: Consecutive horizontal lines at the same height must be **merged** into a single segment.  
For example:  
`[[2,3],[4,5],[7,5],[11,5],[12,7]]`  
is invalid and should be:  
`[[2,3],[4,5],[12,7]]`

---

### Example 1:

**Input:**

```
buildings = [[2,9,10],[3,7,15],[5,12,12],[15,20,10],[19,24,8]]
```

**Output:**

```
[[2,10],[3,15],[7,12],[12,0],[15,10],[20,8],[24,0]]
```

**Explanation:**

- [2,10] marks the start of the first building.
- [3,15] as building 2 overtakes in height.
- [7,12] as building 2 ends and building 3 becomes tallest.
- [12,0] as building 3 ends.
- [15,10] and [20,8] for buildings 4 and 5.
- [24,0] terminates the skyline.

---

### Example 2:

**Input:**

```
buildings = [[0,2,3],[2,5,3]]
```

**Output:**


```
[[0,3],[5,0]]
```


---

### Constraints:

- `1 <= buildings.length <= 10⁴`
- `0 <= lefti < righti <= 2³¹ - 1`
- `1 <= heighti <= 2³¹ - 1`
- `buildings` is sorted by `lefti` in non-decreasing order.

---

### Solution

```cpp
class Solution {
public:
    vector<vector<int>> getSkyline(vector<vector<int>>& buildings) {
        vector<pair<int, int>> events;
        for (auto& b : buildings) {
            // start of building: height negative
            events.emplace_back(b[0], -b[2]);
            // end of building: height positive
            events.emplace_back(b[1], b[2]);
        }

        // sort events
        sort(events.begin(), events.end());

        multiset<int> heights = {0};
        int prevMax = 0;
        vector<vector<int>> result;

        for (auto& [x, h] : events) {
            if (h < 0) {
                // entering building
                heights.insert(-h);
            } else {
                // leaving building
                heights.erase(heights.find(h));
            }

            int currMax = *heights.rbegin();
            if (currMax != prevMax) {
                result.push_back({x, currMax});
                prevMax = currMax;
            }
        }

        return result;
    }
};
```