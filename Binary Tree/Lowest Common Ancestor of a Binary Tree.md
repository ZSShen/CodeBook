
# Problem
### LintCode 88. Lowest Common Ancestor of a Binary Tree
https://www.lintcode.com/problem/lowest-common-ancestor-of-a-binary-tree/description

# Solution
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {

        /**
         *  Use post-order traversal.
         *
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(H), where
         *      H is the height of the tree
         */

        if (!root || root == p || root == q) {
            return root;
        }

        auto l = lowestCommonAncestor(root->left, p, q);
        auto r = lowestCommonAncestor(root->right, p, q);

        if (l && r) {
            return root;
        }

        if (l) {
            return l;
        }
        return r;
    }
};
```