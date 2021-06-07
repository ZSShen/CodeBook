# Problem

### LeetCode 106. Construct Binary Tree from Inorder and Postorder Traversal
https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal

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
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(N)
         *
         * PostOrder: (Left Branch) (Right Branch) Root
         * InOrder  : (Left Branch) Root (Right Branch)
         *
         *       1                        L        R     T
         *     /   \        PostOrder: 4, 5, 2, 6, 7, 3, 1
         *    2     3                  -------  -------
         *   / \   / \                    L     T     R
         *  4   5 6   7     InOrder  : 4, 2, 5, 1, 6, 3, 7
         *                             -------     -------
         */

        unordered_map<int, int> map;
        int n = inorder.size();
        for (int i = 0 ; i < n ; ++i) {
            map[inorder[i]] = i;
        }

        return helper(inorder, postorder, {0, n - 1}, {0, n - 1}, map);
    }

private:
    TreeNode* helper(
            const vector<int>& inorder, const vector<int>& postorder,
            pair<int, int> in_index, pair<int, int> post_index,
            unordered_map<int, int>& map) {

        int in_bgn = in_index.first, in_end = in_index.second;
        if (in_bgn > in_end) {
            return nullptr;
        }
        if (in_bgn == in_end) {
            return new TreeNode(inorder[in_bgn]);
        }

        int post_bgn = post_index.first, post_end = post_index.second;
        int val = postorder[post_end];

        // Find the root node index of the in-order vector.
        int in_mid = map[val];

        auto root = new TreeNode(val);

        root->left = helper(inorder, postorder,
                            {in_bgn, in_mid - 1},
                            {post_bgn, post_bgn + in_mid - in_bgn - 1},
                            map);

        root->right = helper(inorder, postorder,
                             {in_mid + 1, in_end},
                             {post_bgn + in_mid - in_bgn, post_end - 1},
                             map);

        return root;
    }
};
```
