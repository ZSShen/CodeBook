
# Problem
### LintCode 395. Coins in a Line II
https://www.lintcode.com/problem/coins-in-a-line-ii/description

# Solution
```c++
class Solution {
public:
    /**
     * @param values: a vector of integers
     * @return: a boolean which equals to true if the first player will win
     */
    bool firstWillWin(vector<int> &values) {
        // write your code here

        /**
         *  A and B, 2 competitors
         *
         *  Sum(i): The total value of the remained coins covering from the
         *          ith coin to the last one.
         *
         *  Sa: The total value A can aggregate in the current iteration.
         *  Sb: The total value B can aggregate in the next iteration.
         *
         *  When there are (n - i + 1) coins remained, player A has 2 choices.
         *      1. Pick the ith coin,
         *          Sa = values[i] + Sum(i + 1) - Sb'.
         *             = Sum(i) - Sb'.
         *
         *      2. Pick the ith and the (i+1)th coin,
         *          Sa = values[i] + values[i + 1] + Sum(i + 2) - Sb''.
         *             = Sum(i) - Sb''.
         *
         * dp[i]: The maximum value that a person can aggregate when there
         *        are (n - i + 1) coins left.
         *
         * dp[i] = MAX | pick the ith coin                , sum[i] - dp[i + 1]
         *             | pick the ith and the (i+1)th coin, sum[i] - dp[i + 2]
         */

        int n = values.size();
        if (n == 0) {
            return false;
        }
        if (n == 1 || n == 2) {
            return true;
        }

        std::vector<int> sum(n, 0);
        std::vector<int> dp(n, 0);

        sum[n - 1] = values[n - 1];
        sum[n - 2] = sum[n - 1] + values[n - 2];
        dp[n - 1] = values[n - 1];
        dp[n - 2] = dp[n - 1] + values[n - 2];

        for (int i = n - 3 ; i >= 0 ; --i) {
            sum[i] = sum[i + 1] + values[i];

            // values[i] + (sum[i + 1] - dp[i + 1])
            int plan_a = sum[i] - dp[i + 1];

            // values[i] + values[i + 1] + (sum[i + 2) - dp[i + 2])
            int plan_b = sum[i] - dp[i + 2];

            dp[i] = std::max(plan_a, plan_b);
        }

        return dp[0] * 2 > sum[0];
    }
};
```