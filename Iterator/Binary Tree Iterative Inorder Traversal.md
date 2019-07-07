
# Problem
### LintCode 67. Binary Tree Inorder Traversal
https://www.lintcode.com/problem/binary-tree-inorder-traversal/description

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
     * @param root: A Tree
     * @return: Inorder in ArrayList which contains node values.
     */
    vector<int> inorderTraversal(TreeNode * root) {
        // write your code here

        if (!root) {
            return {};
        }

        std::vector<int> ans;
        std::stack<TreeNode*> stk;

        auto curr = root;
        while (curr) {
            stk.push(curr);
            curr = curr->left;
        }

        while (!stk.empty()) {

            auto curr = stk.top();
            stk.pop();

            ans.push_back(curr->val);

            curr = curr->right;
            while (curr) {
                stk.push(curr);
                curr = curr->left;
            }
        }

        return ans;
    }
};
```