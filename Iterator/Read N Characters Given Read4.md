
# Problem
### LeetCode 157. Read N Characters Given Read4
https://leetcode.com/problems/read-n-characters-given-read4

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

        int total = 0, bytes = 0;

        while (total < n && (bytes = read4(buf + total))) {
            total += bytes;
        }

        // Trim the buffer if we have extra bytes
        while (total > n) {
            buf[--total] = 0;
        }

        return total;
    }
};
```