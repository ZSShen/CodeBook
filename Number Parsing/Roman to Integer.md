
# Problem
### LeetCode 13. Roman to Integer
https://leetcode.com/problems/roman-to-integer

# Solution
```c++
class Solution {
public:
    Solution()
        : map({
            {'I', 1},
            {'V', 5},
            {'X', 10},
            {'L', 50},
            {'C', 100},
            {'D', 500},
            {'M', 1000}})
    { }

    int romanToInt(string s) {

        /**
         * Let's scan the string from the tail to the head.
         *
         * 1. If the value of a Roman character is greater than or equal to the
         *    value of its predecessor, the accumulative sum is the value of the
         *    predecessor added by the value of the current character.
         *
         *    e.g.: VI = 1 + 5 = 6
         *          VIII = 1 + 1 + 1 + 5 = 8
         *
         * 2. If the value of a Roman character is less than the value of its
         *    predecessor, the accumulative sum is the value of the predecessor
         *    subtracted by the value of the current character.
         *
         *    e.g.: IV = 5 - 1 = 4
         */

        int n = s.length();
        int sum = map[s[n - 1]];

        for (int i = n - 2 ; i >= 0 ; --i) {
            if (map[s[i]] >= map[s[i + 1]]) {
                sum += map[s[i]];
            } else {
                sum -= map[s[i]];
            }
        }

        return sum;
    }

private:
    unordered_map<char, int> map;
};
```