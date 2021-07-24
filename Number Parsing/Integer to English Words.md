
# Problem
### LeetCode 273. Integer to English Words
https://leetcode.com/problems/integer-to-english-words

# Solution
```c++

constexpr int kRange[] = {100, 1000, 1000 * 1000, 1000 * 1000 * 1000};

const string kRangeTerm[] = {"Hundred", "Thousand", "Million", "Billion"};

const string k20[] = {"One", "Two", "Three", "Four", "Five",
                      "Six", "Seven", "Eight", "Nine", "Ten",
                      "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen",
                      "Sixteen",  "Seventeen", "Eighteen", "Nineteen"};

const string k100[] = {"Twenty", "Thirty", "Forty", "Fifty", "Sixty",
                       "Seventy", "Eighty", "Ninety"};

class Solution {
public:
    string numberToWords(int num) {

        if (num == 0) {
            return "Zero";
        }

        return helper(num).substr(1);
    }

private:
    string helper(int num) {

        if (num == 0) {
            return "";
        }
        if (num < 20) {
            return " " + k20[num - 1];
        }
        if (num < 100) {
            return " " + k100[num / 10 - 2] + helper(num % 10);
        }

        for (int i = 3 ; i >= 0 ; --i) {
            if (num >= kRange[i]) {
                return helper(num / kRange[i]) + " " + kRangeTerm[i] + helper(num % kRange[i]);
            }
        }

        return "";
    }
};
```