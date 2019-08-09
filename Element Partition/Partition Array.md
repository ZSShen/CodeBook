
# Problem
### LintCode 31. Partition Array
https://www.lintcode.com/problem/partition-array/description

# Solution
```c++
class Solution {
public:
    /**
     * @param nums: The integer array you should partition
     * @param k: An integer
     * @return: The index after partition
     */
    int partitionArray(vector<int> &nums, int k) {
        // write your code here

        int n = nums.size();
        int l = 0, r = 0;

        while (r < n) {
            if (nums[r] < k) {
                std::swap(nums[l], nums[r]);
                ++l;
            }
            ++r;
        }

        return l;
    }
};
```