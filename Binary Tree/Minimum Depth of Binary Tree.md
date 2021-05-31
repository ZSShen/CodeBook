
# Problem
### LeetCode 111. Minimum Depth of Binary Tree
https://leetcode.com/problems/minimum-depth-of-binary-tree

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
    int minDepth(TreeNode* root) {

        /**
         *  Use pre-order traversal.
         *
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(H), where
         *      H is the height of the tree
         */

        int ans = INT_MAX;
        runPreOrder(root, 0, ans);
        return ans < INT_MAX ? ans : 0;
    }

private:
    void runPreOrder(TreeNode* root, int depth, int& ans) {

        if (!root) {
            return;
        }

        ++depth;

        if (!root->left && !root->right) {
            ans = min(ans, depth);
        }

        runPreOrder(root->left, depth, ans);
        runPreOrder(root->right, depth, ans);
    }
};
```