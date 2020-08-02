124. Binary Tree Maximum Path Sum

Given a **non-empty** binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain **at least one node** and does not need to go through the root.

**Example 1:**

```
Input: [1,2,3]

       1
      / \
     2   3

Output: 6
```

**Example 2:**

```
Input: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

Output: 42
```

**解**

定义节点node加入路径后能够贡献的最大效益：max_gain

![](../pic/124_gains.png)

算法：

Now everything is ready to write down an algorithm.

- Initiate `max_sum` as the smallest possible integer and call `max_gain(node = root)`.

- Implement

  with a check to continue the old path/to start a new path:

  - Base case : if node is null, the max gain is `0`.
  - Call `max_gain` recursively for the node children to compute max gain from the left and right subtrees : `left_gain = max(max_gain(node.left), 0)` and
    `right_gain = max(max_gain(node.right), 0)`.
  - Now check to continue the old path or to start a new path. To start a new path would cost `price_newpath = node.val + left_gain + right_gain`. Update `max_sum` if it's better to start a new path.
  - For the recursion return the max gain the node and one/zero of its subtrees could add to the current path : `node.val + max(left_gain, right_gain)`.

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
    int max_sum = INT_MIN;
    int maxPathSum(TreeNode* root) {
        max_gain(root);
        return max_sum;
    }
    int max_gain(TreeNode* ptr){
        if(!ptr) return 0;
        int left_val = max(max_gain(ptr->left),0);
        int right_val = max(max_gain(ptr->right),0);
        int cur_gain = ptr->val + left_val + right_val;
        max_sum = max(max_sum, cur_gain);
        return ptr->val + max(left_val, right_val);
    }
};
```

