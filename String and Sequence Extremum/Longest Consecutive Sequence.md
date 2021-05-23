
# Problem
### LeetCode 128. Longest Consecutive Sequence
https://leetcode.com/problems/longest-consecutive-sequence

# Solution
```c++
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(N)
         */

        unordered_set<int> set(nums.begin(), nums.end());

        int ans = 0;
        while (!set.empty()) {
            auto it = set.begin();
            int num = *it;
            int local = 1;
            set.erase(it);

            int next = num + 1;
            while (set.count(next) == 1) {
                set.erase(next);
                ++local;
                ++next;
            }

            next = num - 1;
            while (set.count(next) == 1) {
                set.erase(next);
                ++local;
                --next;
            }

            ans = max(ans, local);
        }

        return ans;
    }
};
```