
# Problem
### LeetCode 158. Read N Characters Given Read4 II - Call multiple times
https://leetcode.com/problems/read-n-characters-given-read4-ii-call-multiple-times

# Solution
```c++
/**
 * The read4 API is defined in the parent class Reader4.
 *     int read4(char *buf4);
 */

class Solution {
public:
    /**
     * @param buf Destination buffer
     * @param n   Number of characters to read
     * @return    The number of actual characters read
     */
    int read(char *buf, int n) {

        // Check if there is any extra byte reamined in the previous round.
        int total = 0;
        while (total < n && !stack.empty()) {
            buf[total++] = stack.top();
            stack.pop();
        }

        // Read the file.
        int read = 0;
        while (total < n && (read = read4(buf + total)) > 0) {
            total += read;
        }

        // Push the extra bytes into the stack.
        while (total > n) {
            stack.emplace(buf[--total]);
        }

        return total;
    }

private:
    stack<char> stack;
};
```