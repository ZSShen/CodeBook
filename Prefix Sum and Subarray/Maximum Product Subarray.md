
# Problem
### Leetcode 152. Maximum Product Subarray
https://leetcode.com/problems/maximum-product-subarray/

# Solution
```c++
class Solution {
public:
    int maxProduct(vector<int>& nums) {

        int min_sofar = 1;
        int max_sofar = 1;

        int ans = nums[0];
        int n = nums.size();

        for (int i = 0 ; i < n ; ++i) {
            int e = nums[i];
            int max_curr = max(max(min_sofar * e, max_sofar * e), e);
            int min_curr = min(min(min_sofar * e, max_sofar * e), e);

            ans = max(ans, max_curr);
            min_sofar = min_curr;
            max_sofar = max_curr;
        }

        return ans;
    }
};
```