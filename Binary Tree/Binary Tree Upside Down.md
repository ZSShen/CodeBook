
# Problem
### LintCode 649. Binary Tree Upside Down
https://www.lintcode.com/problem/binary-tree-upside-down/description

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
     * @param root: the root of binary tree
     * @return: new root
     */
    TreeNode * upsideDownBinaryTree(TreeNode * root) {
        // write your code here

        /**
         *
         *  1 -- 3           1 -- 3      4 -- 2 -- 1         4
         *  |                |           |    |             / \
         *  2 -- 5  =>  4 -- 2       =>  5    3       =>   5   2
         *  |           |                                     / \
         *  4           5                                    3   1
         *
         *
         *  1. Find the very left offspring, which will be the root of the
         *     up-side-downed tree.
         *
         *  2. For each node, if it has the right sibling, we need to change
         *     the sibling as the left child of the current node.
         *
         *     Moreover, if its parent is not null, we need to change the parent
         *     as the right child of the current node.
         */

        if (!root) {
            return nullptr;
        }

        return runPreOrder(root, nullptr);
    }

private:
    TreeNode* runPreOrder(TreeNode* curr, TreeNode* parent) {

        TreeNode* new_root = nullptr;

        if (curr->left) {
            new_root = runPreOrder(curr->left, curr);
        }

        // To record the new root.
        if (!new_root) {
            new_root = curr;
        }

        // For the original root node.
        if (!parent) {
            return new_root;
        }

        // The current node has a right sibling.
        if (parent->right) {
            curr->left = parent->right;
        }

        // Change the parent as the right child of the current node.
        curr->right = parent;
        parent->left = parent->right = nullptr;

        return new_root;
    }
};

```