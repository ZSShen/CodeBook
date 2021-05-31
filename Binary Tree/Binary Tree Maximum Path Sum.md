
# Problem
### LeetCode 124. Binary Tree Maximum Path Sum
https://leetcode.com/problems/binary-tree-maximum-path-sum

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
    int maxPathSum(TreeNode* root) {

        /**
         *  Consider the following tree rooted by T. If we want to generate
         *  a maximum path sum which passes T, we need to check thw following
         *  cases.
         *
         *      T       Let L denote the maximum path sum returned from the
         *     / \      left branch of T.
         *    /   \
         *   /\   /\    Let R denote the maximum path sum returned from the
         *  /__\ /__\   right branch of T.
         *
         *              Then, the candidate sum for T would be:
         *              MAX { T, T + L, T + R, T + L + R }
         *
         *              And the path sum that we need to return to the parent
         *              level is:
         *              MAX { T, T + L, T + R }
         *
         *
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(H), where
         *      H is the height of the tree
         */

        int opt = INT_MIN;
        findPath(root, opt);
        return opt;
    }

private:
    int findPath(TreeNode* root, int& opt) {

        if (!root) {
            return 0;
        }

        int l = findPath(root->left, opt);
        int r = findPath(root->right, opt);

        opt = max(opt, root->val);
        opt = max(opt, root->val + r);
        opt = max(opt, root->val + l);
        opt = max(opt, root->val + r + l);

        return max(root->val, max(root->val + l, root->val + r));
    }
};
```