
# Problem
### LeetCode 670. Maximum Swap
https://leetcode.com/problems/maximum-swap

# Solution
```c++
class Solution {
public:
    int maximumSwap(int num) {

        /**
         *  TC: O(1)
         *  SC: O(1)
         *
         *  We record the last occurance index of each digit.
         *  The objective is to put the greatest digit to the
         *  most significant position.
         *
         *  Input: 1 1 7 6
         *
         *  last[1] = 1
         *  last[7] = 2
         *  last[6] = 3
         *
         *  For the first position, i = 0, we start by checking
         *  from the maximum digit 9 to the minimum digit 0.
         *  We observe that last[7] = 2 and 2 > 0, so this implies
         *  that we can swap nums[0] with nums[2], making the result
         *  number 7 1 1 6.
         */

        string str = to_string(num);

        vector<int> index(10);
        int n = str.length();
        for (int i = 0 ; i < n ; ++i) {
            index[str[i] - '0'] = i;
        }

        for (int i = 0 ; i < n ; ++i) {
            for (int j = 9 ; j > str[i] - '0' ; --j) {
                if (index[j] > i) {
                    swap(str[i], str[index[j]]);
                    return stoi(str);
                }
            }
        }

        return num;
    }
};
```