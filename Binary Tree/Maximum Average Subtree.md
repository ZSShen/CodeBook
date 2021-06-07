
# Problem
### LeetCode 1120. Maximum Average Subtree
https://leetcode.com/problems/maximum-average-subtree

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

struct Record {
    int size = 0;
    int sum = 0;
};


class Solution {
public:
    double maximumAverageSubtree(TreeNode* root) {

        /**
         *  TC: O(N), where
         *      N is the number of nodes
         *
         *  SC: O(H), where
         *      H is the height of the tree
         */

        double ans = 0;
        runPostOrder(root, ans);
        return ans;
    }

private:
    Record runPostOrder(TreeNode* root, double& ans) {

        if (!root) {
            return Record();
        }

        auto l = runPostOrder(root->left, ans);
        auto r = runPostOrder(root->right, ans);

        Record record;
        record.size = 1 + l.size + r.size;
        record.sum = root->val + l.sum + r.sum;

        double avg = static_cast<double>(record.sum) / record.size;
        ans = max(avg, ans);

        return record;
    }
};
```
