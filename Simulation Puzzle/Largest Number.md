
# Problem
### LintCode 184. Largest Number
https://www.lintcode.com/problem/largest-number/description

# Solution
```c++
class Solution {
public:
    /**
     * @param nums: A list of non negative integers
     * @return: A string
     */
    string largestNumber(vector<int> &nums) {
        // write your code here

        /**
         * A: 65, B: 6
         *
         * A + B = 656
         * B + A = 665
         *
         * B + A > A + B => B > A
         */

        std::unordered_map<int, int> radixes;
        for (int num : nums) {
            if (radixes.count(num) == 1) {
                continue;
            }
            int radix = (num > 0) ?
                static_cast<int>(std::floor(std::log10(num))) + 1 : 1;
            radixes[num] = radix;
        }

        std::sort(nums.begin(), nums.end(),
            [&] (const auto& a, const auto& b) {
                long ab = a * static_cast<long>(std::pow(10, radixes[b])) + b;
                long ba = b * static_cast<long>(std::pow(10, radixes[a])) + a;
                return ab > ba;
            }
        );

        std::string ans;
        for (int num : nums) {
            ans += std::to_string(num);
        }

        // For the case that the string content is 000...
        if (ans[0] == '0') {
            return "0";
        }

        return ans;
    }
};
```
