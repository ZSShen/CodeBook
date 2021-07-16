
# Problem
### LeetCode 772. Basic Calculator III
https://leetcode.com/problems/basic-calculator-iii

# Solution
```c++
class Solution {
public:
    Solution()
        : map({{'+', 1}, {'-', 1}, {'*', 2}, {'/', 2}, {'(', 3}, {')', 0}})
    { }

    int calculate(string s) {

        /**
         *  TC: O(N), where
         *      N is the string length
         *
         *  SC: O(N)
         */

        stack<char> operators;
        stack<long> operands;

        int n = s.length(), i = 0;

        while (i < n) {
            if (s[i] == ' ') {
                ++i;
                continue;
            }

            if (isdigit(s[i])) {
                long res = 0;

                while (i < n && isdigit(s[i])) {
                    res = res * 10 + (s[i++] - '0');
                }

                operands.emplace(res);
                continue;
            }

            while (!operators.empty() &&
                    operators.top() != '(' &&
                    map[operators.top()] >= map[s[i]]) {

                long op2 = operands.top();
                operands.pop();

                long op1 = operands.top();
                operands.pop();

                long res = eval(op1, op2, operators.top());
                operands.emplace(res);
                operators.pop();
            }

            if (s[i] == ')') {
                operators.pop();
                ++i;
            } else {
                operators.emplace(s[i++]);
            }
        }

        while (!operators.empty()) {

            long op2 = operands.top();
            operands.pop();

            long op1 = operands.top();
            operands.pop();

            long res = eval(op1, op2, operators.top());
            operands.emplace(res);
            operators.pop();
        }

        return operands.top();
    }

private:
    unordered_map<char, int> map;

    long eval(long op1, long op2, char op) {
        long res = 0;

        switch (op) {
            case '+':
                res = op1 + op2;
                break;
            case '-':
                res = op1 - op2;
                break;
            case '*':
                res = op1 * op2;
                break;
            case '/':
                res = op1 / op2;
                break;
        }

        return res;
    }
};
```