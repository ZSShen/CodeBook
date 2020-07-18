
# Problem
### LeetCode 1123. Lowest Common Ancestor of Deepest Leaves
https://leetcode.com/problems/lowest-common-ancestor-of-deepest-leaves/

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
    TreeNode* lcaDeepestLeaves(TreeNode* root) {
        unordered_map<TreeNode*, int> memo;
        return runPostOrder(root, memo);
    }

private:
    TreeNode* runPostOrder(
        TreeNode* root, unordered_map<TreeNode*, int>& memo) {

        if (!root) {
            return nullptr;
        }

        auto l = getHeight(root->left, memo);
        auto r = getHeight(root->right, memo);
        if (l == r) {
            return root;
        }

        if (l > r) {
            return runPostOrder(root->left, memo);
        }
        return runPostOrder(root->right, memo);
    }

    int getHeight(TreeNode* root, unordered_map<TreeNode*, int>& memo) {

        if (!root) {
            return 0;
        }

        if (memo.count(root)) {
            return memo[root];
        }

        auto l = getHeight(root->left, memo);
        auto r = getHeight(root->right, memo);

        int h = max(l, r) + 1;
        memo[root] = h;
        return h;
    }
};
```