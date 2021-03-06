# LeetCode: 156. 上下翻转二叉树

[TOC]

## 1、题目描述

给定一个二叉树，其中所有的右节点要么是具有兄弟节点（拥有相同父节点的左节点）的叶节点，要么为空，将此二叉树上下翻转并将它变成一棵树， 原来的右节点将转换成左叶节点。返回新的根。

**例子:**

输入:  `[1,2,3,4,5]`

 ```
    1
   / \
  2   3
 / \
4   5
 ```



输出: 返回二叉树的根 [4,5,2,#,#,3,1]

```
   4
  / \
 5   2
    / \
   3   1  
```

**说明:**

对 [4,5,2,#,#,3,1] 感到困惑? 下面详细介绍请查看 二叉树是如何被序列化的。

二叉树的序列化遵循层次遍历规则，当没有节点存在时，'#' 表示路径终止符。

这里有一个例子:

```
   1
  / \
 2   3
    /
   4
    \
     5
```

上面的二叉树则被序列化为 `[1,2,3,#,#,4,#,#,5].`



## 2、解题思路

- 递归法，一直寻找到最终的左节点
- 然后将右节点变为左节点
- 根节点变为右节点，并将根节点的子节点设置为None



```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def upsideDownBinaryTree(self, root: TreeNode) -> TreeNode:
        if not root or not root.left:
            return root

        left = root.left
        right = root.right
        res = self.upsideDownBinaryTree(left)
        left.left = right
        left.right = root
        root.left = None
        root.right = None
        return res
```

