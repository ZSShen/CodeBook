
# Problem
### LintCode 246. Binary Tree Path Sum II
https://www.lintcode.com/problem/binary-tree-path-sum-ii/description

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
    vector<vector<int>> pathSum(TreeNode* root, int target) {

        /**
         *  Use post-order traversal.
         *
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(H), where
         *      H is the height of the tree
         */

        vector<int> config;
        vector<vector<int>> ans;
        runPreOrder(root, target, 0, config, ans);
        return ans;
    }

private:
    void runPreOrder(
            TreeNode* root, int target,
            int prefix, vector<int>& config, vector<vector<int>>& ans) {

        if (!root) {
            return;
        }

        prefix += root->val;
        config.emplace_back(root->val);

        // Check the leaf node.
        if (!root->left && !root->right) {
            if (prefix == target) {
                ans.emplace_back(config);
            }
            config.pop_back();
            return;
        }

        runPreOrder(root->left, target, prefix, config, ans);
        runPreOrder(root->right, target, prefix, config, ans);

        config.pop_back();
    }
};
```