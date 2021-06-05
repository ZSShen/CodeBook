# Problem

### LeetCode 103. Binary Tree Zigzag Level Order Traversal
https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal

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
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(N)
         *
         * We can use 2 stacks to control the traversal.
         *
         * In a specific level, we consume all the nodes collected in the first
         * stack and explore the children of those nodes.
         *
         * If the level number is even, e.g. 0 and 2, we explore the children
         * from the very left side to the very right side and push them onto
         * the second stack.
         *
         * If the level number is odd, e.g. 1 and 3, we explore the children
         * from the very right side to the very left side and push them onto
         * the second stack.
         *
         * Upon finishing consuming the nodes collected in the first stack,
         * we override the first stack with the content of the second stack.
         *
         *      Visualization:
         *
         *      ------>-----> level 0  L -> R
         *                  |
         *      <-----<-----| level 1  R -> L
         *      |
         *      |----->-----> level 2  L -> R
         *
         */

        if (!root) {
            return {};
        }

        vector<vector<int>> ans;

        stack<TreeNode*> stk;
        stk.emplace(root);

        int round = 0;

        while (!stk.empty()) {
            stack<TreeNode*> next;
            vector<int> level;

            int n = stk.size();
            for (int i = 0 ; i < n ; ++i) {
                auto node = stk.top();
                stk.pop();

                level.emplace_back(node->val);

                if (round % 2 == 0) {
                    if (node->left) {
                        next.emplace(node->left);
                    }
                    if (node->right) {
                        next.emplace(node->right);
                    }
                } else {
                    if (node->right) {
                        next.emplace(node->right);
                    }
                    if (node->left) {
                        next.emplace(node->left);
                    }
                }
            }

            ++round;
            stk = move(next);
            ans.emplace_back(move(level));
        }

        return ans;
    }
};
```
