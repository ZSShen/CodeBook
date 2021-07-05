
# Problem
### LeetCode 145. Binary Tree Postorder Traversal
https://leetcode.com/problems/binary-tree-postorder-traversal

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
    vector<int> postorderTraversal(TreeNode* root) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(N)
         */

        vector<int> ans;

        stack<TreeNode*> stk;
        collectNodes(root, stk);

        while (!stk.empty()) {
            auto node = stk.top();
            stk.pop();

            ans.emplace_back(node->val);

            if (!stk.empty() && node == stk.top()->left) {
                collectNodes(stk.top()->right, stk);
            }
        }

        return ans;
    }

private:
    void collectNodes(TreeNode* root, stack<TreeNode*>& stk) {

        while (root) {
            stk.emplace(root);

            if (root->left) {
                root = root->left;
            } else {
                root = root->right;
            }
        }
    }
};
```