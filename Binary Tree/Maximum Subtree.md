
# Problem
### LintCode 628. Maximum Subtree
https://www.lintcode.com/problem/maximum-subtree/description

# Solution
```c++
struct Result {
    int sum;
    TreeNode* root;

    Result()
      : sum(0), root(nullptr)
    { }

    Result(int sum, TreeNode* root)
      : sum(sum), root(root)
    { }
};


class Solution {
public:
    /**
     * @param root: the root of binary tree
     * @return: the root of the maximum subtree
     */
    TreeNode * findSubtree(TreeNode * root) {
        // write your code here

        Result opt(INT_MIN, nullptr);
        runPostOrder(root, opt);
        return opt.root;
    }

private:
    Result runPostOrder(TreeNode* root, Result& opt) {

        if (!root) {
            return Result();
        }

        auto l = runPostOrder(root->left, opt);
        auto r = runPostOrder(root->right, opt);

        int sum = root->val + l.sum + r.sum;
        if (sum > opt.sum) {
            opt.sum = sum;
            opt.root = root;
        }

        return Result(sum, root);
    }
};
```
