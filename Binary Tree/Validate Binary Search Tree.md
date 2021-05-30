
# Problem
### LeetCode 98. Validate Binary Search Tree
https://leetcode.com/problems/validate-binary-search-tree

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
    bool isValidBST(TreeNode* root) {

        /**
         *  Use Pre-Order traversal.
         *
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(H), where
         *      H is the height of the tree
         */

        return runPreOrder(root, nullptr, nullptr);
    }

private:
    bool runPreOrder(TreeNode* root, TreeNode* lo, TreeNode* hi) {

        if (!root) {
            return true;
        }

        if (lo && root->val <= lo->val) {
            return false;
        }
        if (hi && root->val >= hi->val) {
            return false;
        }

        if (!runPreOrder(root->left, lo, root)) {
            return false;
        }
        return runPreOrder(root->right, root, hi);
    }
};
```