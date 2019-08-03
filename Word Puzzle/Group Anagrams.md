
# Problem
### LintCode 772. Group Anagrams
https://www.lintcode.com/problem/group-anagrams/description

# Solution
```c++
class Solution {
public:
    /**
     * @param strs: the given array of strings
     * @return: The anagrams which have been divided into groups
     */
    vector<vector<string>> groupAnagrams(vector<string> &strs) {
        // write your code here

        std::unordered_map<std::string, std::vector<std::string>> groups;

        for (const auto& word : strs) {
            auto key(word);
            std::sort(key.begin(), key.end());
            groups[key].push_back(word);
        }

        std::vector<std::vector<std::string>> ans;
        for (auto& pair : groups) {
            ans.emplace_back(std::move(pair.second));
        }

        return ans;
    }
};
```