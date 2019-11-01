
# Problem
### LintCode 661. Convert BST to Greater Tree
https://www.lintcode.com/problem/convert-bst-to-greater-tree/description

# Solution
```c++
/**
 * Definition of TreeNode:
 * class TreeNode {
 * public:
 *     int val;
 *     TreeNode *left, *right;
 *     TreeNode(int val) {
 *         this->val = val;
 *         this->left = this->right = NULL;
 *     }
 * }
 */

class Solution {
public:
    /**
     * @param root: the root of binary tree
     * @return: the new root
     */
    TreeNode * convertBST(TreeNode * root) {
        // write your code here

        int sum = 0;
        runReversedInOrder(root, sum);
        return root;
    }

private:
    void runReversedInOrder(TreeNode* root, int& sum) {

        if (!root) {
            return;
        }

        runReversedInOrder(root->right, sum);
        sum += root->val;
        root->val = sum;
        runReversedInOrder(root->left, sum);
    }
};
```