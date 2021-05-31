
# Problem
### LeetCode 104. Maximum Depth of Binary Tree
https://leetcode.com/problems/maximum-depth-of-binary-tree

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
    int maxDepth(TreeNode* root) {

        /**
         *  Use pre-order traversal.
         *
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(H), where
         *      H is the height of the tree
         */

        int ans = INT_MIN;
        helper(root, 0, ans);
        return ans > INT_MIN ? ans : 0;
    }

private:
    void helper(TreeNode *root, int depth, int& ans) {

        if (!root) {
            return;
        }

        ++depth;

        if (!root->left && !root->right) {
            ans = max(ans, depth);
        }

        helper(root->left, depth, ans);
        helper(root->right, depth, ans);
    }
};
```