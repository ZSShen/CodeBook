
# Problem
### LeetCode 380. Insert Delete GetRandom O(1)
https://leetcode.com/problems/insert-delete-getrandom-o1

# Solution
```c++
class RandomizedSet {
public:
    /** Initialize your data structure here. */
    RandomizedSet() {

    }

    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    bool insert(int val) {

        if (map.count(val) == 1) {
            return false;
        }

        records.emplace_back(val);
        map[val] = records.size() - 1;

        return true;
    }

    /** Removes a value from the set. Returns true if the set contained the specified element. */
    bool remove(int val) {

        if (map.count(val) == 0) {
            return false;
        }

        int idx = map[val];

        // Swap the last element with the one
        // we intend to delete
        swap(records[idx], records.back());

        records.pop_back();

        // Update the index for the swapped element.
        // Note: Update and then delete to cover the
        // case that the swapped element and the deleted
        // one are actually the same.
        map[records[idx]] = idx;
        map.erase(val);

        return true;
    }

    /** Get a random element from the set. */
    int getRandom() {
        int idx = random() % records.size();
        return records[idx];
    }

private:
    vector<int> records;
    unordered_map<int, int> map;
};

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet* obj = new RandomizedSet();
 * bool param_1 = obj->insert(val);
 * bool param_2 = obj->remove(val);
 * int param_3 = obj->getRandom();
 */
```