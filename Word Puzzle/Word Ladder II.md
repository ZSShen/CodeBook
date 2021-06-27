
# Problem
### LintCode 121. Word Ladder II
https://www.lintcode.com/problem/word-ladder-ii/description

# Solution
```c++
class Solution {
public:
    vector<vector<string>> findLadders(string begin, string end, vector<string>& words) {

        /**
         *  TC: O(N * K * 25), where
         *      N is the number of words
         *      K is average word length
         *
         *  SC: O(N * K)
         *                  dot(3) -- dog(4)
         *                /                 \
         * hit(1) - hot(2)                   cog(5)
         *                \                 /
         *                  lot(3) -- log(4)
         *
         */

        unordered_set<string> dict(words.begin(), words.end());
        unordered_map<string, unordered_set<string>> graph;
        unordered_map<string, int> discovery;
        discovery[begin] = 0;

        buildGraph(begin, end, dict, graph, discovery);

        vector<string> config;
        config.emplace_back(begin);
        vector<vector<string>> ans;

        findPath(begin, end, 0, graph, discovery, config, ans);

        return ans;
    }

private:
    void buildGraph(
            const string& begin, const string& end,
            unordered_set<string>& dict,
            unordered_map<string, unordered_set<string>>& graph,
            unordered_map<string, int>& discovery) {

        queue<string> q;
        q.emplace(begin);

        int level = 0;

        while (!q.empty()) {
            int n = q.size();
            ++level;

            for (int i = 0 ; i < n ; ++i) {
                auto src = q.front();
                q.pop();

                auto dst(src);
                int l = dst.length();

                for (int j = 0 ; j < l ; ++j) {
                    char backup = dst[j];

                    for (char ch = 'a' ; ch <= 'z' ; ++ch) {
                        dst[j] = ch;

                        if (dict.count(dst) == 0) {
                            continue;
                        }

                        // Add an edge.
                        graph[src].emplace(dst);

                        // The first time we visit this word.
                        if (discovery.count(dst) == 0) {
                            discovery[dst] = level;
                            q.emplace(dst);
                        }
                    }

                    dst[j] = backup;
                }
            }
        }
    }

    void findPath(
            const string& begin, const string& end,
            int level,
            unordered_map<string, unordered_set<string>>& graph,
            unordered_map<string, int>& discovery,
            vector<string>& config,
            vector<vector<string>>& ans) {

        if (begin == end) {
            ans.emplace_back(config);
            return;
        }

        for (const auto& neighbor : graph[begin]) {
            if (discovery[neighbor] != level + 1) {
                continue;
            }

            config.emplace_back(neighbor);
            findPath(neighbor, end, level + 1, graph, discovery, config, ans);
            config.pop_back();
        }
    }
};
```