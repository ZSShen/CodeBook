
# Problem
### 134. LRU Cache
https://www.lintcode.com/problem/lru-cache/description

# Solution
```c++
#include <list>

class LRUCache {
public:
    /*
    * @param capacity: An integer
    */LRUCache(int capacity)
      : size(0),
        capacity(capacity) {
        // do intialization if necessary
    }

    /*
     * @param key: An integer
     * @return: An integer
     */
    int get(int key) {
        // write your code here

        if (refs.count(key) == 0) {
            return -1;
        }

        auto iter = refs[key];
        int value = iter->second;

        list.erase(iter);
        list.push_front(std::make_pair(key, value));
        refs[key] = list.begin();

        return value;
    }

    /*
     * @param key: An integer
     * @param value: An integer
     * @return: nothing
     */
    void set(int key, int value) {
        // write your code here

        if (refs.count(key) == 0) {
            list.push_front(std::make_pair(key, value));
            refs[key] = list.begin();

            ++size;
            if (size == capacity + 1) {
                auto iter = --list.end();
                int expired_key = iter->first;

                list.erase(iter);
                refs.erase(expired_key);

                --size;
            }
            return;
        }

        auto iter = refs[key];
        list.erase(iter);
        list.push_front(std::make_pair(key, value));
        refs[key] = list.begin();
    }

private:
    int size;
    int capacity;
    std::list<std::pair<int, int>> list;
    std::unordered_map<int, std::list<std::pair<int, int>>::iterator> refs;
};
```