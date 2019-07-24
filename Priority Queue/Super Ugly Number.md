
# Problem
### LintCode 518. Super Ugly Number
https://www.lintcode.com/problem/super-ugly-number/description

# Solution
```c++

class Solution {
public:
    /**
     * @param n: a positive integer
     * @param primes: the given prime list
     * @return: the nth super ugly number
     */
    int nthSuperUglyNumber(int n, vector<int> &primes) {
        // write your code here

        std::set<long, std::less<long>> queue;
        queue.insert(1);

        long nth = 0;
        for (int i = 0 ; i < n ; ++i) {
            nth = *queue.begin();
            queue.erase(nth);

            for (int prime : primes) {
                queue.insert(nth * prime);
            }
        }

        return nth;
    }
};
```
