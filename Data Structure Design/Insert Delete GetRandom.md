
# Problem
### 657. Insert Delete GetRandom O(1)
https://www.lintcode.com/problem/insert-delete-getrandom-o1/description

# Solution
```c++
/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet obj = new RandomizedSet();
 * bool param = obj.insert(val);
 * bool param = obj.remove(val);
 * int param = obj.getRandom();
 */


class RandomizedSet {
public:
    RandomizedSet() {
        // do intialization if necessary
        srand(time(nullptr));
    }

    /*
     * @param val: a value to the set
     * @return: true if the set did not already contain the specified element or false
     */
    bool insert(int val) {
        // write your code here

        if (refs.count(val) == 1) {
            return false;
        }

        nums.push_back(val);
        refs[val] = nums.size() - 1;
        return true;
    }

    /*
     * @param val: a value from the set
     * @return: true if the set contained the specified element or false
     */
    bool remove(int val) {
        // write your code here

        if (refs.count(val) == 0) {
            return false;
        }

        // If the number that we want to remove is just the last element of the
        // vector, we simply clean the relevant entries.
        int index = refs[val];
        if (index == nums.size() - 1) {
            refs.erase(val);
            nums.pop_back();
            return true;
        }

        // Otherwise, we swap the last element with the to be removed element
        // and update the indexing structure for that last element.
        std::swap(nums.back(), nums[index]);
        refs[nums[index]] = index;
        nums.pop_back();
        return true;
    }

    /*
     * @return: Get a random element from the set
     */
    int getRandom() {
        // write your code here

        int index = random() % nums.size();
        return nums[index];
    }

private:
    std::vector<int> nums;
    std::unordered_map<int, int> refs;
};

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet obj = new RandomizedSet();
 * bool param = obj.insert(val);
 * bool param = obj.remove(val);
 * int param = obj.getRandom();
 */
```