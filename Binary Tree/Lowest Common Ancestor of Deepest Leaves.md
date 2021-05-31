
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

        /**
         *  Use post-order traversal.
         *
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
    pair<TreeNode*, int> runPostOrder(TreeNode* root) {
        if (!root) {
            return {nullptr, -1};
        }

        auto l = runPostOrder(root->left);
        auto r = runPostOrder(root->right);

        if (l.second == r.second) {
            return {root, l.second + 1};
        }

        if (l.second > r.second) {
            return {l.first, l.second + 1};
        }
        return {r.first, r.second + 1};
    }
};
```