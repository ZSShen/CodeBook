
# Problem
### LintCode 453. Flatten Binary Tree to Linked List
https://www.lintcode.com/problem/flatten-binary-tree-to-linked-list/

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
    void flatten(TreeNode* root) {

        /**
         *         1
         *        / \
         *       2   5
         *      / \   \
         *     3   4   6
         *
         *         1
         *          \
         *           2
         *          / \
         *         3   4
         *              \
         *               5
         *                \
         *                 6
         *
         *          1
         *           \
         *            2
         *             \
         *              3
         *               \
         *                4
         *                 \
         *                  5
         *                   \
         *                    6
         */

        while (curr) {
            if (curr->left) {
                auto pivot = curr->left;
                while (pivot->right) {
                    pivot = pivot->right;
                }

                pivot->right = curr->right;
                curr->right = curr->left;
                curr->left = nullptr;
            }
            curr = curr->right;
        }
    }
};
```