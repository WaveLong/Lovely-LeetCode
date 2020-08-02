114. Flatten Binary Tree to Linked List

Medium

1992257Add to ListShare

Given a binary tree, flatten it to a linked list in-place.

For example, given the following tree:

```
    1
   / \
  2   5
 / \   \
3   4   6
```

The flattened tree should look like:

```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

**Solution**

后序遍历。调整左边->调整右边->合并结果

```c++
class Solution {
public:
    void flatten(TreeNode* root) {
        if(root == NULL)return;
        flatten(root->left);
        flatten(root->right);
        TreeNode* tmp = root->right;
        root->right = root->left;
        root->left = NULL;
        TreeNode *p = root;
        while(p->right)p = p->right;
        p->right = tmp;
    }
};
```

