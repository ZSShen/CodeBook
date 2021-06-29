
# Problem
### LeetCode 212. Word Search II
https://leetcode.com/problems/word-search-ii

# Solution
```c++
struct Node {
    bool is_word = false;
    unordered_map<char, shared_ptr<Node>> branch;
};


class Solution {
public:
    Solution()
        : directs({{1, 0}, {-1, 0}, {0, 1}, {0, -1}})
    { }

    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {

        /**
         *  TC: O(M * N * (3^L)), where
         *      M is the number of rows
         *      N is the number of columns
         *      L is the word length
         *
         *  SC: O(L)
         */

        auto root = buildTrie(words);

        int m = board.size();
        int n = board[0].size();

        unordered_set<string> ans;

        for (int x = 0 ; x < m ; ++x) {
            for (int y = 0 ; y < n ; ++y) {
                string config;
                backTracking(x, y, m, n, root, board, config, ans);
            }
        }

        return vector<string>(ans.begin(), ans.end());
    }

private:
    vector<vector<int>> directs;

    shared_ptr<Node> buildTrie(const vector<string>& words) {

        auto root = make_shared<Node>();

        for (const auto& word : words) {
            auto curr = root;

            for (char ch : word) {
                if (curr->branch.count(ch) == 0) {
                    curr->branch[ch] = make_shared<Node>();
                }
                curr = curr->branch[ch];
            }

            curr->is_word = true;
        }

        return root;
    }

    void backTracking(
            int x, int y, int m, int n,
            shared_ptr<Node> curr,
            vector<vector<char>>& board,
            string& config,
            unordered_set<string>& ans) {

        char ch = board[x][y];
        config.push_back(ch);

        if (curr->branch.count(ch) == 0) {
            config.pop_back();
            return;
        }

        curr = curr->branch[ch];

        // If this is the tail of a word.
        if (curr->is_word) {
            ans.emplace(config);

            // Mark the word as visited so we won't collect duplicates.
            curr->is_word = false;
        }

        board[x][y] = 0;

        for (const auto& d : directs) {
            int nx = x + d[0];
            int ny = y + d[1];

            if (!(nx >= 0 && ny >= 0 && nx < m && ny < n) ||
                board[nx][ny] == 0) {
                continue;
            }

            backTracking(nx, ny, m, n, curr, board, config, ans);
        }

        config.pop_back();
        board[x][y] = ch;
    }
};
```