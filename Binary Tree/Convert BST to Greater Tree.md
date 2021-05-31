
# Problem
### LeetCode 538. Convert BST to Greater Tree
https://leetcode.com/problems/convert-bst-to-greater-tree

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
    TreeNode* convertBST(TreeNode* root) {

        if (!root) {
            return root;
        }

        int sum = 0;
        runReverseInOrder(root, sum);
        return root;
    }

private:
    void runReverseInOrder(TreeNode* root, int& sum) {

        if (!root) {
            return;
        }

        runReverseInOrder(root->right, sum);
        sum += root->val;
        root->val = sum;
        runReverseInOrder(root->left, sum);
    }
};
```