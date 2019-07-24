
# Problem
### LintCode 4. Ugly Number II
https://www.lintcode.com/problem/ugly-number-ii/description

# Solution
```c++

class Solution {
public:
    /**
     * @param n: An integer
     * @return: return a  integer as description.
     */
    int nthUglyNumber(int n) {
        // write your code here

        /**
         *          Priority Queue
         *
         * 1st: 1   2, 3, 5
         * 2nd: 2   3, 4, 5, 6, 10
         * 3rd: 3   4, 6, 9, 10, 15
         *
         *      ...
         */

        std::set<long, std::less<long>> queue;
        queue.insert(1);

        long nth = 0;
        for (int i = 0 ; i < n ; ++i) {
            nth = *queue.begin();
            queue.erase(nth);

            queue.insert(nth * 2);
            queue.insert(nth * 3);
            queue.insert(nth * 5);
        }

        return nth;
    }
};

```