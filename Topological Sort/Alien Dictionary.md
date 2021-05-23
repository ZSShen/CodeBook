
# Problem
### LeetCode 269. Alien Dictionary
https://leetcode.com/problems/alien-dictionary/

# Solution
```c++
class Solution {
public:
    string alienOrder(vector<string>& words) {

        /**
         * TC: O(n * W), where
         *      n is the number of words
         *      W is the average length of a word
         *
         * SC: O(V + E), where
         *      V is the number of nodes
         *      E is the number of edges
         */

        int n = words.size();
        unordered_map<char, unordered_set<char>> graph;
        unordered_map<char, int> indeg;

        for (const auto& word : words) {
            for (char c : word) {
                indeg[c] = 0;
            }
        }

        for (int i = 1 ; i < n ; ++i) {

            const auto& src = words[i - 1];
            const auto& dst = words[i];

            int len = min(src.length(), dst.length());
            bool diff = false;

            for (int j = 0 ; j < len ; ++j) {
                char s = src[j];
                char t = dst[j];

                if (s != t) {
                    diff = true;
                    if (graph[s].count(t) == 0) {
                        graph[s].emplace(t);
                        ++indeg[t];
                    }
                    break;
                }
            }

            if (!diff && src.length() > dst.length()) {
                return "";
            }
        }

        // Run topological sort.
        queue<char> queue;
        for (const auto& pair : indeg) {
            if (pair.second == 0) {
                queue.emplace(pair.first);
            }
        }

        string ans;
        while (!queue.empty()) {
            char s = queue.front();
            queue.pop();

            ans.push_back(s);

            for (char t : graph[s]) {
                --indeg[t];
                if (indeg[t] == 0) {
                    queue.emplace(t);
                }
            }
        }

        return ans.length() == indeg.size() ? ans : "";
    }
};
```