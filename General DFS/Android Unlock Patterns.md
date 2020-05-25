
# Problem
### LintCode 909. Android Unlock Patterns
https://www.lintcode.com/problem/android-unlock-patterns/description

# Solution
```c++
class Solution {
public:
    /**
     * @param m: an integer
     * @param n: an integer
     * @return: the total number of unlock patterns of the Android lock screen
     */
    int numberOfPatterns(int m, int n) {
        // Write your code here

        vector<vector<int>> rule(10, vector<int>(10, 0));

        rule[1][3] = rule[3][1] = 2;
        rule[4][6] = rule[6][4] = 5;
        rule[7][9] = rule[9][7] = 8;

        rule[1][7] = rule[7][1] = 4;
        rule[2][8] = rule[8][2] = 5;
        rule[3][9] = rule[9][3] = 6;

        rule[1][9] = rule[9][1] = rule[3][7] = rule[7][3] = 5;

        int ans = 0;
        for (int i = m ; i <= n ; ++i) {
            vector<bool> visit(10, false);
            ans += runBackTracking(rule, i, visit, 1) * 4;
            ans += runBackTracking(rule, i, visit, 2) * 4;
            ans += runBackTracking(rule, i, visit, 5);
        }

        return ans;
    }

private:
    int runBackTracking(const auto& rule, int step, auto& visit, int src) {

        if (step == 1) {
            return 1;
        }

        int count = 0;
        visit[src] = true;

        for (int dst = 1 ; dst <= 9 ; ++dst) {
            if (visit[dst]) {
                continue;
            }
            if (rule[src][dst] != 0 && !visit[rule[src][dst]]) {
                continue;
            }
            count += runBackTracking(rule, step - 1, visit, dst);
        }

        visit[src] = false;
        return count;
    }
};
```