---
title: 144-binary-tree-preorder-traversal
tags: 在河之洲,算法,小书匠
grammar_cjkRuby: true
---


# problem
[144-binary-tree-preorder-traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/#/description)
# solution
用递归的方式进行先序遍历 

```cpp
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        preorderVisit(root, result);
        return result;
    }
    void preorderVisit(TreeNode *node, vector<int> &ret)
    {
        if (node!=NULL)
        {
            ret.push_back(node->val);
            preorderVisit(node->left,ret);
            preorderVisit(node->right,ret);
        }
    }
```


借助栈结构的迭代法

```cpp
   vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        if (root == NULL)
            return result;
        stack<TreeNode *> toVisit;
        toVisit.push(root);
        while (!toVisit.empty())
        {
            TreeNode *tmp = toVisit.top();
            result.push_back(tmp->val);
            toVisit.pop();
            if (tmp->right)
                toVisit.push(tmp->right);
            if (tmp->left)
                toVisit.push(tmp->left);
        }
        return result;
        
    }

```