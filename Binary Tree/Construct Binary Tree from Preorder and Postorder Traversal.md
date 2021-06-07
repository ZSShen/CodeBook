# Problem

### LeetCode 889. Construct Binary Tree from Preorder and Postorder Traversal
https://leetcode.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal

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
    TreeNode* constructFromPrePost(vector<int>& pre, vector<int>& post) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(N)
         *
         *  PreOrder : Root (Left Branch) (Right Branch)
         *  PostOrder: (Left Branch) (Right Branch) Root
         *
         *                                *
         *      1                      T  P  L        R
         *    /   \         PreOrder : 1, 2, 4, 5, 3, 6, 7
         *   2     3                      -------  -------
         *  / \   / \                     L  P     R     T
         * 4   5 6   7      PostOrder: 4, 5, 2, 6, 7, 3, 1
         *                             -------  -------
         */

        unordered_map<int, int> map;
        int n = post.size();
        for (int i = 0 ; i < n ; ++i) {
            map[post[i]] = i;
        }

        return helper(pre, post, {0, n - 1}, {0, n - 1}, map);
    }

private:
    TreeNode* helper(
            const vector<int>& pre, const vector<int>& post,
            pair<int, int> pre_index, pair<int, int> post_index,
            unordered_map<int, int>& map) {

        int pre_bgn = pre_index.first, pre_end = pre_index.second;
        if (pre_bgn > pre_end) {
            return nullptr;
        }
        if (pre_bgn == pre_end) {
            return new TreeNode(pre[pre_bgn]);
        }

        int post_bgn = post_index.first, post_end = post_index.second;
        int val = pre[pre_bgn];

        // Find the index of the first node of the left branch of the
        // pre-order vector.
        int pivot = map[pre[pre_bgn + 1]];
        int size_left = pivot - post_bgn + 1;

        auto root = new TreeNode(val);

        root->left = helper(pre, post,
                            {pre_bgn + 1, pre_bgn + size_left},
                            {post_bgn, post_bgn + size_left - 1},
                            map);

        root->right = helper(pre, post,
                             {pre_bgn + size_left + 1, pre_end},
                             {post_bgn + size_left, post_end - 1},
                             map);

        return root;
    }
};
```
