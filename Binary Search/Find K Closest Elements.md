
# Problem
### LeetCode 658. Find K Closest Elements
https://leetcode.com/problems/find-k-closest-elements

# Solution
```c++
class Solution {
public:
    vector<int> findClosestElements(vector<int>& arr, int k, int x) {

        /**
         *  TC: O(logN + K), where
         *      N is the number of elements
         *
         *  SC: O(1)
         */

        int n = arr.size();
        int l = 0, r = n - 1;

        while (l + 1 < r) {
            int m = l + (r - l) / 2;
            if (arr[m] <= x) {
                l = m;
            } else {
                r = m;
            }
        }

        // Check arr[l] and arr[r] to decide
        // the closest element.
        if (arr[r] - x < x - arr[l]) {
            ++l;
            ++r;
        }

        if (k == 1) {
            return {arr[l]};
        }

        --k;
        while (k > 0) {
            if (r == n || (l > 0 && x - arr[l - 1] <= arr[r] - x)) {
                --l;
            } else {
                ++r;
            }
            --k;
        }

        vector<int> ans;
        for (int i = l ; i < r ; ++i) {
            ans.emplace_back(arr[i]);
        }
        return ans;
    }
};
```