# Problem

### LeetCode 993. Cousins in Binary Tree
https://leetcode.com/problems/cousins-in-binary-tree

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
    bool isCousins(TreeNode* root, int x, int y) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(H), where
         *      H is the height of the tree
         */

        TreeNode *px = nullptr, *py = nullptr;
        int dx = 0, dy = 0;
        runPreOrder(root, nullptr, x, y, 0, px, py, dx, dy);

        return (dx == dy) && (px != py);
    }

private:
    void runPreOrder(
            TreeNode *curr, TreeNode *parent,
            int x, int y, int depth,
            TreeNode* &px, TreeNode* &py, int& dx, int& dy) {

        if (!curr) {
            return;
        }
        ++depth;

        if (curr->val == x) {
            dx = depth;
            px = parent;
        }
        if (curr->val == y) {
            dy = depth;
            py = parent;
        }

        runPreOrder(curr->left, curr, x, y, depth, px, py, dx, dy);
        runPreOrder(curr->right, curr, x, y, depth, px, py, dx, dy);
    }
};
```
