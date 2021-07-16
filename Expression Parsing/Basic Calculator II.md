
# Problem
### LeetCode 227. Basic Calculator II
https://leetcode.com/problems/basic-calculator-ii

# Solution
```c++
class Solution {
public:
    Solution()
        : map({{'+', 1}, {'-', 1}, {'*', 2}, {'/', 2}})
    { }

    int calculate(string s) {

        /**
         *  TC: O(N), where
         *      N is the string length
         *
         *  SC: O(N)
         */

        stack<long> operands;
        stack<char> operators;

        int n = s.length(), i = 0;

        while (i < n) {
            if (s[i] == ' ') {
                ++i;
                continue;
            }

            if (isdigit(s[i])) {
                long num = 0;
                while (i < n && isdigit(s[i])) {
                    num = num * 10 + (s[i++] - '0');
                }
                operands.emplace(num);
                continue;
            }

            while (!operators.empty() &&
                   map[operators.top()] >= map[s[i]]) {
                long op2 = operands.top();
                operands.pop();
                long op1 = operands.top();
                operands.pop();
                operands.emplace(eval(op1, op2, operators.top()));
                operators.pop();
            }

            operators.emplace(s[i++]);
        }

        while (!operators.empty()) {
            long op2 = operands.top();
            operands.pop();
            long op1 = operands.top();
            operands.pop();
            operands.emplace(eval(op1, op2, operators.top()));
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