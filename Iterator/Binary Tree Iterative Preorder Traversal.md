# Problem

### LeetCode 144. Binary Tree Preorder Traversal
https://leetcode.com/problems/binary-tree-preorder-traversal

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
    vector<int> preorderTraversal(TreeNode* root) {

        /**
         *  TC: O(N), where
         *      N is the number of tree nodes.
         *
         *  SC: O(N)
         */

        if (!root) {
            return {};
        }

        vector<int> ans;

        stack<TreeNode*> stk;
        stk.emplace(root);

        while (!stk.empty()) {
            auto node = stk.top();
            stk.pop();

            ans.emplace_back(node->val);

            if (node->right) {
                stk.emplace(node->right);
            }
            if (node->left) {
                stk.emplace(node->left);
            }
        }

        return ans;
    }
};
```
