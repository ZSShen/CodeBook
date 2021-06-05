
# Problem
### LeetCode 110. Balanced Binary Tree
https://leetcode.com/problems/balanced-binary-tree

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
    bool isBalanced(TreeNode* root) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(H), where
         *      H is the height of the tree
         */

        auto res = runPostOrder(root);
        return res.first;
    }

private:
    pair<bool, int> runPostOrder(TreeNode* root) {

        if (!root) {
            return {true, 0};
        }

        auto l = runPostOrder(root->left);
        if (!l.first) {
            return {false, -1};
        }

        auto r = runPostOrder(root->right);
        if (!r.first) {
            return {false, -1};
        }

        int diff = abs(l.second - r.second);
        if (diff > 1) {
            return {false, -1};
        }

        return {true, max(l.second, r.second) + 1};
    }
};
```