
# Problem
### LintCode 900. Closest Binary Search Tree Value

https://www.lintcode.com/problem/closest-binary-search-tree-value/description

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
     * @param root: the given BST
     * @param target: the given target
     * @return: the value in the BST that is closest to the target
     */
    int closestValue(TreeNode * root, double target) {
        // write your code here

        /**
         * lower_bound: the max value which is less than target.
         * upper_bound: the min value which is greater than or equal to target.
         */

        auto lower = findLowerBound(root, target);
        auto upper = findUpperBound(root, target);

        if (!lower) {
            return upper->val;
        }
        if (!upper) {
            return lower->val;
        }

        if ((target - static_cast<double>(lower->val)) <
            (static_cast<double>(upper->val) - target)) {
            return lower->val;
        }

        return upper->val;
    }

private:
    TreeNode* findLowerBound(TreeNode* root, double target) {

        if (!root) {
            return nullptr;
        }

        if (target <= root->val) {
            return findLowerBound(root->left, target);
        }

        // target > root->val
        auto lower = findLowerBound(root->right, target);
        if (lower) {
            return lower;
        }

        return root;
    }

    TreeNode* findUpperBound(TreeNode* root, double target) {

        if (!root) {
            return nullptr;
        }

        if (root->val < target) {
            return findUpperBound(root->right, target);
        }

        // target <= root->val
        auto upper = findUpperBound(root->left, target);
        if (upper) {
            return upper;
        }

        return root;
    }
};
```
