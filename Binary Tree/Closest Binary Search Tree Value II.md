# Problem

### LintCode 71. Binary Tree Zig Zag Level Order Traversal

https://www.lintcode.com/problem/binary-tree-zigzag-level-order-traversal/description

# Solution
```c++
class Solution {
public:
    /**
     * @param root: the given BST
     * @param target: the given target
     * @param k: the given k
     * @return: k values in the BST that are closest to the target
     */
    vector<int> closestKValues(TreeNode * root, double target, int k) {
        // write your code here

        /**
         *  target = 19.
         *  k = 3
         *
         *          20
         *         /  \
         *       15    30
         *      /  \    \
         *    10    17   35
         *   /  \    \
         *  5   12    18
         *
         *
         *  pred: 20
         *  succ: 15, 17, 18
         *
         *  20 -> 15 -> 17 -> 18
         */

        std::stack<TreeNode*> pred;
        std::stack<TreeNode*> succ;

        auto curr = root;
        while (curr) {
            if (target >= curr->val) {
                pred.push(curr);
                curr = curr->right;
            } else {
                succ.push(curr);
                curr = curr->left;
            }
        }

        std::vector<int> ans;
        for (int i = 0 ; i < k ; ++i) {

            if (pred.empty()) {
                ans.push_back(succ.top()->val);
                getSuccessors(succ);
                continue;
            }

            if (succ.empty()) {
                ans.push_back(pred.top()->val);
                getPredecessors(pred);
                continue;
            }

            auto p = pred.top();
            auto s = succ.top();
            if (std::abs(p->val - target) < std::abs(s->val - target)) {
                ans.push_back(p->val);
                getPredecessors(pred);
            } else {
                ans.push_back(s->val);
                getSuccessors(succ);
            }
        }

        return ans;
    }

private:
    void getPredecessors(std::stack<TreeNode*>& pred) {

        auto curr = pred.top();
        pred.pop();

        if (curr->left) {
            curr = curr->left;
            pred.push(curr);

            curr = curr->right;
            while (curr) {
                pred.push(curr);
                curr = curr->right;
            }
        }
    }

    void getSuccessors(std::stack<TreeNode*>& succ) {

        auto curr = succ.top();
        succ.pop();

        if (curr->right) {
            curr = curr->right;
            succ.push(curr);

            curr = curr->left;
            while (curr) {
                succ.push(curr);
                curr = curr->left;
            }
        }
    }
};
```
