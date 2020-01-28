
# Problem
### LintCode 994. Contiguous Array
https://www.lintcode.com/problem/contiguous-array/description

# Solution
```c++
class Solution {
public:
    /**
     * @param nums: a binary array
     * @return: the maximum length of a contiguous subarray
     */
    int findMaxLength(vector<int> &nums) {
        // Write your code here

        unordered_map<int, int> map{{0, -1}};
        int prefix = 0;
        int max = 0;
        int n = nums.size();

        for (int i = 0 ; i < n ; ++i) {
            int num = nums[i];

            if (num == 1) {
                ++prefix;
            } else {
                --prefix;
            }

            auto iter = map.find(prefix);
            if (iter != map.end()) {
                max = std::max(max, i - iter->second);
            } else {
                map[prefix] = i;
            }
        }

        return max;
    }
};
```