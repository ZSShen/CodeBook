
# Problem
### LintCode 1311. Lowest Common Ancestor of a Binary Search Tree
https://www.lintcode.com/problem/lowest-common-ancestor-of-a-binary-search-tree/description

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
         *  TC: O(N), where
         *      N is the number of nodes
         *  SC: O(H), where
         *      H is the height of the tree
         */

        while (root) {
            if (root->val < p->val && root->val < q->val) {
                root = root->right;
            } else if (root->val > p->val && root->val > q->val) {
                root = root->left;
            } else {
                break;
            }
        }

        return root;
    }
};
```