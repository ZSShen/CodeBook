
# Problem
### LeetCode 94. Binary Tree Inorder Traversal
https://leetcode.com/problems/binary-tree-inorder-traversal

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
    vector<int> inorderTraversal(TreeNode* root) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(N)
         */

        vector<int> ans;

        stack<TreeNode*> stk;
        while (root) {
            stk.emplace(root);
            root = root->left;
        }

        while (!stk.empty()) {
            auto node = stk.top();
            stk.pop();

            ans.emplace_back(node->val);

            node = node->right;
            while (node) {
                stk.emplace(node);
                node = node->left;
            }
        }

        return ans;
    }
};
```