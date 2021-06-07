# Problem

### LeetCode 101. Symmetric Tree
https://leetcode.com/problems/symmetric-tree/solution


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
    bool isSymmetric(TreeNode* root) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(H), where
         *      H is the height of the tree
         */

        return helper(root, root);
    }

private:
    bool helper(TreeNode* left, TreeNode* right) {

        if (!left || !right) {
            return left == right;
        }

        if (left->val != right->val) {
            return false;
        }

        return helper(left->left, right->right) &&
               helper(left->right, right->left);
    }
};
```
