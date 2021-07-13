
# Problem
### LeetCode 146. LRU Cache
https://leetcode.com/problems/lru-cache

# Solution
```c++
class LRUCache {
public:
    LRUCache(int capacity)
        : capacity(capacity)
    { }

    int get(int key) {

        if (map.count(key) == 0) {
            return -1;
        }

        auto it = map[key];
        int value = it->second;

        // Update the liveness of the node.
        records.erase(it);
        records.push_front({key, value});
        map[key] = records.begin();

        return value;
    }

    void put(int key, int value) {

        if (map.count(key) == 1) {
            records.erase(map[key]);
        }

        records.push_front({key, value});
        map[key] = records.begin();

        // If the cache is full, we need to erase the
        // list tail.
        if (records.size() > capacity) {
            int tail_key = records.back().first;
            records.pop_back();
            map.erase(tail_key);
        }
    }

private:
    int capacity;
    list<pair<int, int>> records;
    unordered_map<int, list<pair<int, int>>::iterator> map;
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```