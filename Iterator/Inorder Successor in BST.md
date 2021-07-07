
# Problem
### LeetCode 285. Inorder Successor in BST
https://leetcode.com/problems/inorder-successor-in-bst

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
    TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {

        /**
         *  TC: O(H), where
         *      H is the tree height
         *
         *  SC: O(1)
         */

        TreeNode* succ = nullptr;

        while (root) {
            if (root->val > p->val) {
                succ = root;
                root = root->left;
            } else {
                root = root->right;
            }
        }

        return succ;
    }
};
```