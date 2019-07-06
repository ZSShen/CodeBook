
# Problem
### LeetCode 958. Check Completeness of a Binary Tree
https://leetcode.com/problems/check-completeness-of-a-binary-tree/

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

struct Record {
    TreeNode* node;
    int label;

    Record(TreeNode* node, int label)
      : node(node), label(label)
    { }
};


class Solution {
public:
    bool isCompleteTree(TreeNode* root) {

        // Level Order Traversal + Label Counter

        if (!root) {
            return true;
        }

        int count = 0;
        std::queue<Record> queue;
        queue.push(Record(root, 1));

        while (!queue.empty()) {

            int size = queue.size();
            for (int i = 0 ; i < size ; ++i) {
                auto rec = queue.front();
                queue.pop();

                auto node = rec.node;
                int label = rec.label;

                // Check the label order.
                ++count;
                if (count != label) {
                    return false;
                }

                if (node->left) {
                    queue.push(Record(node->left, label * 2));
                }
                if (node->right) {
                    queue.push(Record(node->right, label * 2 + 1));
                }
            }
        }

        return true;
    }
};
```