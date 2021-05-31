
# Problem
### LintCode 138. Subarray Sum
https://www.lintcode.com/problem/subarray-sum

# Solution
```c++
class Solution {
public:
    /**
     * @param nums: A list of integers
     * @return: A list of integers includes the index of the first number and the index of the last number
     */
    vector<int> subarraySum(vector<int> &nums) {
        // write your code here

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(N)
         *
         *  preix(i) = num[0] + num[1] + ... + nums[i]
         *  sum(i, j) = prefix(j) - prefix(i - 1)
         *             = nums[i] + num[i + 1] + ... + num[j]
         *
         *  sum(i, j) = 0
         *  => prefix(j) - prefix(i - 1) = 0
         *  => prefix(j) = prefix(i - 1)
         */

        unordered_map<int, int> map;
        map[0] = -1;

        int prefix = 0;
        int n = nums.size();

        for (int i = 0 ; i < n ; ++i) {
            prefix += nums[i];

            if (map.count(prefix) == 1) {
                return {map[prefix] + 1, i};
            }
        }

        return {-1, -1};
    }
};
```