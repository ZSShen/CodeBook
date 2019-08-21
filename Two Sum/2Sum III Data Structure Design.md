
# Problem
### LintCode 607. Two Sum III - Data structure design
https://www.lintcode.com/problem/two-sum-iii-data-structure-design/description

# Solution
```c++
class TwoSum {
public:
    /**
     * @param number: An integer
     * @return: nothing
     */
    void add(int number) {
        // write your code here

        set.insert(number);
    }

    /**
     * @param value: An integer
     * @return: Find if there exists any pair of numbers which sum is equal to the value.
     */
    bool find(int value) {
        // write your code here

        for (int src : set) {
            int dst = value - src;
            int freq = (src != dst) ? 1 : 2;
            if (set.count(dst) >= freq) {
                return true;
            }
        }

        return false;
    }

private:
    std::unordered_multiset<int> set;
};

```