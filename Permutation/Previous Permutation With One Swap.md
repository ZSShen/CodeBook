
# Problem
### LeetCode 1053. Previous Permutation With One Swap
https://leetcode.com/problems/previous-permutation-with-one-swap

# Solution
```c++
class Solution {
public:
    vector<int> prevPermOpt1(vector<int>& arr) {

        /**
         *  TC: O(N), where
         *      N is the number of elements
         *
         *  SC: O(1)
         */

        int n = arr.size(), l;
        for (l = n - 2 ; l >= 0 ; --l) {
            if (arr[l] > arr[l + 1]) {
                break;
            }
        }

        // Input is already the smallest permutation.
        if (l == -1) {
            return arr;
        }

        int num = -1, r;
        for (int i = n - 1 ; i > l ; --i) {
            if (arr[i] < arr[l] && arr[i] >= num) {
                num = arr[i];
                r = i;
            }
        }

        swap(arr[l], arr[r]);
        return arr;
    }
};
```