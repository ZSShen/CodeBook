
# Problem
### LintCode 491. Palindrome Number
https://www.lintcode.com/problem/palindrome-number/description

# Solution
```c++
class Solution {
public:
    /**
     * @param num: a positive number
     * @return: true if it's a palindrome or false
     */
    bool isPalindrome(int num) {
        // write your code here

        long mirror = 0;

        long copy = num;
        while (copy > 0) {
            mirror *= 10;
            mirror += copy % 10;
            copy /= 10;
        }

        return mirror == num;
    }
};
```