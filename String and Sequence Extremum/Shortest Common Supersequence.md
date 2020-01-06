
# Problem
### LeetCode 1092. Shortest Common Supersequence
https://leetcode.com/problems/shortest-common-supersequence/

# Solution
```c++
class Solution {
public:
    string shortestCommonSupersequence(string s1, string s2) {

        /**
            dp[i][j]: The length of the SCS of the prefix of S1 ending at offset i
                      and the prefix of S2 ending at offset j.

            dp[i][j] = | if S1[i] == S2[j], 1 + dp[i - 1][j - 1]
                       | Otherwise        , 1 + MIN{dp[i - 1][j], dp[i][j - 1]}
         */

        int n1 = s1.length();
        int n2 = s2.length();

        vector<vector<int>> dp(n1 + 1, vector<int>(n2 + 1, 0));
        vector<vector<char>> trace(n1 + 1, vector<char>(n2 + 1, 0));

        for (int i = 1 ; i <= n2 ; ++i) {
            dp[0][i] = i;
            trace[0][i] = S2;
        }
        for (int i = 1 ; i <= n1 ; ++i) {
            dp[i][0] = i;
            trace[i][0] = S1;
        }

        for (int i = 1 ; i <= n1 ; ++i) {
            for (int j = 1 ; j <= n2 ; ++j) {
                if (s1[i - 1] == s2[j - 1]) {
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                    trace[i][j] = C;
                } else {
                    if (dp[i - 1][j] < dp[i][j - 1]) {
                        dp[i][j] = 1 + dp[i - 1][j];
                        trace[i][j] = S1;
                    } else {
                        dp[i][j] = 1 + dp[i][j - 1];
                        trace[i][j] = S2;
                    }
                }
            }
        }

        string scs;
        int r = n1, c = n2;
        while (r > 0 || c > 0) {
            if (trace[r][c] == S1) {
                scs.push_back(s1[--r]);
            } else if (trace[r][c] == S2) {
                scs.push_back(s2[--c]);
            } else {
                scs.push_back(s1[--r]);
                --c;
            }
        }

        std::reverse(scs.begin(), scs.end());
        return scs;
    }

private:
    enum {
        S1 = 1,
        S2 = 2,
        C = 3
    };
};
```