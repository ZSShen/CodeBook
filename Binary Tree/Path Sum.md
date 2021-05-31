
# Problem
### LeetCode 112. Path Sum
https://leetcode.com/problems/path-sum

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
    bool hasPathSum(TreeNode* root, int sum) {

        int prefix = 0;
        return runPreOrder(root, prefix, sum);
    }

private:
    bool runPreOrder(TreeNode* root, int prefix, int target) {

        if (!root) {
            return false;
        }

        prefix += root->val;

        if (!root->left && !root->right) {
            return prefix == target;
        }

        if (runPreOrder(root->left, prefix, target)) {
            return true;
        }
        return runPreOrder(root->right, prefix, target);
    }
};
```