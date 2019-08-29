
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

        int ans;
        double min_diff = INT_MAX;

        while (root) {
            double diff = std::abs(target - static_cast<double>(root->val));
            if (diff < min_diff) {
                min_diff = diff;
                ans = root->val;
            }

            if (root->val <= target) {
                root = root->right;
            } else {
                root = root->left;
            }
        }

        return ans;
    }
};
```
