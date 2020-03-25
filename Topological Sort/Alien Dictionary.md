
# Problem
### LintCode 892. Alien Dictionary
https://www.lintcode.com/problem/alien-dictionary/description

# Solution
```c++
class Solution {
public:
    string alienOrder(vector<string>& words) {

        unordered_map<char, unordered_set<char>> graph;
        unordered_map<char, int> indeg;

        int n = words.size();
        for (int i = 1 ; i <= n ; ++i) {
            const auto& src = words[i - 1];
            const auto& dst = (i < n) ? words[i] : "";

            int ls = src.length();
            int ld = dst.length();

            int is = 0, id = 0;
            bool found_diff = false;
            while (is < ls || id < ld) {
                char cs = (is < ls) ? src[is++] : 0;
                char cd = (id < ld) ? dst[id++] : 0;

                if (cs && indeg.count(cs) == 0) {
                    indeg[cs] = 0;
                }
                if (cd && indeg.count(cd) == 0) {
                    indeg[cd] = 0;
                }

                if (!cs || !cd) {
                    continue;
                }

                if (!found_diff && cs != cd) {
                    if (graph[cs].count(cd) == 0) {
                        graph[cs].emplace(cd);
                        ++indeg[cd];
                    }
                    found_diff = true;
                }
            }
        }

        queue<char> queue;
        for (const auto& pair: indeg) {
            if (pair.second == 0) {
                queue.emplace(pair.first);
            }
        }

        string order;
        while (!queue.empty()) {
            char src = queue.front();

            queue.pop();
            order.push_back(src);

            for (char dst : graph[src]) {
                --indeg[dst];
                if (indeg[dst] == 0) {
                    queue.emplace(dst);
                }
            }
        }

        return order.length() == indeg.size() ? order : "";
    }
};
```