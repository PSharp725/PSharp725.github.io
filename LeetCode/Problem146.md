---
title: "LeetCode Problem 146: LRU Cache"
---

# LRU Cache

### Problem Description

Design a data structure that implements the **Least Recently Used (LRU)** cache mechanism.

Implement the `LRUCache` class:

- `LRUCache(int capacity)` initializes the cache with a positive size capacity.
- `int get(int key)` returns the value of the key if it exists, otherwise returns -1.
- `void put(int key, int value)` updates the value of the key if it exists; otherwise, adds the key-value pair to the cache.  
  If the number of keys exceeds the capacity, evicts the **least recently used** key.

Both `get` and `put` must run in **O(1)** average time complexity.

---

### Example 1:

**Input:**

```
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]  
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
```

**Output:**

```
[null, null, null, 1, null, -1, null, -1, 3, 4]
```

**Explanation:**

LRUCache lRUCache = new LRUCache(2)  
lRUCache.put(1, 1)     → cache is {1=1}  
lRUCache.put(2, 2)     → cache is {1=1, 2=2}  
lRUCache.get(1)        → returns 1  
lRUCache.put(3, 3)     → evicts key 2 → cache is {1=1, 3=3}  
lRUCache.get(2)        → returns -1 (not found)  
lRUCache.put(4, 4)     → evicts key 1 → cache is {4=4, 3=3}  
lRUCache.get(1)        → returns -1 (not found)  
lRUCache.get(3)        → returns 3  
lRUCache.get(4)        → returns 4

---

### Constraints:

- 1 <= capacity <= 3000  
- 0 <= key <= 10⁴  
- 0 <= value <= 10⁵  
- At most 2 × 10⁵ calls will be made to `get` and `put`.

---

### Solution

```cpp
class LRUCache {
private:
    int cap;
    list<pair<int, int>> lru;
    unordered_map<int, list<pair<int, int>>::iterator> cache;

public:
    LRUCache(int capacity) {
        cap = capacity;
    }

    int get(int key) {
        if (cache.find(key) == cache.end())
            return -1;

        // Move the accessed node to the front
        auto it = cache[key];
        int val = it->second;
        lru.erase(it);
        lru.push_front({key, val});
        cache[key] = lru.begin();
        return val;
    }

    void put(int key, int value) {
        if (cache.find(key) != cache.end()) {
            // Update existing node
            lru.erase(cache[key]);
        } else if (lru.size() == cap) {
            // Evict least recently used
            int oldKey = lru.back().first;
            lru.pop_back();
            cache.erase(oldKey);
        }

        lru.push_front({key, value});
        cache[key] = lru.begin();
    }
};
```