
# Problem
### LintCode 838. Subarray Sum Equals K
https://www.lintcode.com/problem/subarray-sum-equals-k/description

# Solution
```c++
class Solution {
public:
    /**
     * @param nums: a list of integer
     * @param k: an integer
     * @return: return an integer, denote the number of continuous subarrays whose sum equals to k
     */
    int subarraySumEqualsK(vector<int> &nums, int k) {
        // write your code here

        /**
         *  sum(i, j) = prefix(j) -  prefix(i - 1) = k
         *  => prefix(i - 1) = prefix(j) - k
         */

        std::unordered_map<int, int> map;
        map[0] = 1;

        int sum = 0;
        int count = 0;
        for (int num : nums) {
            sum += num;
            count += map[sum - k];
            ++map[sum];
        }

        return count;
    }
};
```