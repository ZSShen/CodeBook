
# Problem
### LintCode 448. Inorder Successor in BST
https://www.lintcode.com/problem/inorder-successor-in-bst/description

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
    /*
     * @param root: The root of the BST.
     * @param p: You need find the successor node of p.
     * @return: Successor of p.
     */
    TreeNode * inorderSuccessor(TreeNode * root, TreeNode * p) {
        // write your code here

        if (!root || !p) {
            return nullptr;
        }

        if (p->right) {
            auto curr = p->right;
            TreeNode* pred;
            while (curr) {
                pred = curr;
                curr = curr->left;
            }
            return pred;
        }

        auto curr = root;
        TreeNode* pred = nullptr;
        while (curr != p) {
            if (p->val < curr->val) {
                pred = curr;
                curr = curr->left;
            } else {
                curr = curr->right;
            }
        }

        return pred;
    }
};
```