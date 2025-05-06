---
title: "LeetCode Problem 207: Course Schedule"
---

# Course Schedule

### Problem Description

You are given `numCourses` courses labeled from `0` to `numCourses - 1`, and a list of prerequisite pairs where `prerequisites[i] = [ai, bi]` means **you must take course `bi` before course `ai`**.

Return `true` if it's possible to finish all courses. Otherwise, return `false`.

---

### Example 1:

**Input:**

```
numCourses = 2  
prerequisites = [[1, 0]]
```

**Output:**

```
true
```

**Explanation:**  
There are two courses: 0 and 1.  
To take course 1, you must first take course 0. No cycles exist, so it's possible to complete both.

---

### Example 2:

**Input:**

```
numCourses = 2  
prerequisites = [[1, 0], [0, 1]]
```

**Output:**

```
false
```

**Explanation:**  
There is a cycle: to take course 0, you need course 1; to take course 1, you need course 0.  
This makes it impossible to finish all courses.

---

### Constraints:

- 1 <= numCourses <= 2000  
- 0 <= prerequisites.length <= 5000  
- prerequisites[i].length == 2  
- 0 <= ai, bi < numCourses  
- All prerequisites are unique

---

### Solution

```cpp
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> graph(numCourses);
        vector<int> indegree(numCourses, 0);

        // Build graph and indegree count
        for (auto& p : prerequisites) {
            graph[p[1]].push_back(p[0]);
            indegree[p[0]]++;
        }

        queue<int> q;
        for (int i = 0; i < numCourses; ++i) {
            if (indegree[i] == 0) {
                q.push(i);
            }
        }

        int completed = 0;
        while (!q.empty()) {
            int course = q.front();
            q.pop();
            completed++;

            for (int next : graph[course]) {
                indegree[next]--;
                if (indegree[next] == 0) {
                    q.push(next);
                }
            }
        }

        return completed == numCourses;
    }
};
```