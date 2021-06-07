
# Problem
### LeetCode 270. Closest Binary Search Tree Value
https://leetcode.com/problems/closest-binary-search-tree-value

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
    int closestValue(TreeNode* root, double target) {

        double g_diff = INT_MAX;
        int ans = root->val;
        helper(root, target, g_diff, ans);
        return ans;
    }

private:
    void helper(TreeNode* root, double target, double& g_diff, int& ans) {

        if (!root) {
            return;
        }

        double diff = abs(static_cast<double>(root->val) - target);
        if (diff < g_diff) {
            g_diff = diff;
            ans = root->val;
        }

        if (target >= root->val) {
            helper(root->right, target, g_diff, ans);
        } else {
            helper(root->left, target, g_diff, ans);
        }
    }
};
```
