# Problem

### LeetCode 536. Construct Binary Tree from String
https://leetcode.com/problems/construct-binary-tree-from-string

# Solution
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* str2tree(string s) {

        /**
         *  TC: O(N), where
         *      N is the string length
         *
         *  SC: O(N)
         */

        int bgn = 0;
        return runPreOrder(s, bgn, s.length());
    }

private:
    TreeNode* runPreOrder(
            const string& s,
            int& bgn, int end) {

        if (bgn == end) {
            return nullptr;
        }

        bool is_neg = false;
        if (s[bgn] == '-') {
            is_neg = true;
            ++bgn;
        }

        int val = 0;
        while (isdigit(s[bgn])) {
            val = val * 10 + s[bgn] - '0';
            ++bgn;
        }
        if (is_neg) {
            val = -val;
        }

        auto root = new TreeNode(val);

        if (bgn < end && s[bgn] == '(') {
            root->left = runPreOrder(s, ++bgn, end);
        }
        if (bgn < end && s[bgn] == '(') {
            root->right = runPreOrder(s, ++bgn, end);
        }

        // skip ')'
        ++bgn;
        return root;
    }
};
```
