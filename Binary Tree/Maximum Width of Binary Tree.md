
# Problem
### LeetCode 662. Maximum Width of Binary Tree
https://leetcode.com/problems/maximum-width-of-binary-tree

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
    int widthOfBinaryTree(TreeNode* root) {

        /**
         *  Use level order BFS. When labeling tree nodes, make sure to
         *  normalize labels with regard to the minimum label of a level.
         *
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(N)
         */

        queue<pair<TreeNode*, int>> q;
        q.push({root, 1});

        int ans = 1;

        while (!q.empty()) {
            int n = q.size();

            int left = INT_MAX;
            int right = INT_MIN;
            int base = q.front().second;
            z
            for (int i = 0 ; i < n ; ++i) {
                auto record = q.front();
                q.pop();

                int id = record.second - base;
                left = min(left, id);
                right = max(right, id);

                auto node = record.first;
                if (node->left) {
                    q.push({node->left, id << 1});
                }
                if (node->right) {
                    q.push({node->right, (id << 1) + 1});
                }
            }

            ans = max(ans, right - left + 1);
        }

        return ans;
    }
};
```