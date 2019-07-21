
# Problem
### LintCode 604. Window Sum
https://www.lintcode.com/problem/window-sum/description

# Solution
```c++
class Solution {
public:
    /**
     * @param nums: a list of integers.
     * @param k: length of window.
     * @return: the sum of the element inside the window at each moving.
     */
    vector<int> winSum(vector<int> &nums, int k) {
        // write your code here

        int n = nums.size();
        if (n == 0 || k == 0) {
            return {};
        }

        std::vector<int> ans;

        int sum = 0;
        for (int i = 0 ; i < k ; ++i) {
            sum += nums[i];
        }
        ans.push_back(sum);

        int l = 0, r = k;
        while (r < n) {
            sum += nums[r];
            sum -= nums[l];

            ans.push_back(sum);

            ++l;
            ++r;
        }


        return ans;
    }
};
```