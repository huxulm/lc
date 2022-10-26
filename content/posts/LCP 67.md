---
title: LCP 67.装饰树
slug: jijian-by-endlesscheng-4oqo
author: endlesscheng
date: 2022-10-07T11:14:39Z
---
# 极简写法：调用自身
 
> [原题 LCP 67.装饰树](https://leetcode.cn/problems/KnLfVT)
调用自身。

```py [sol1-Python]
class Solution:
    def expandBinaryTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if root.left: root.left = TreeNode(-1, left=self.expandBinaryTree(root.left))
        if root.right: root.right = TreeNode(-1, right=self.expandBinaryTree(root.right))
        return root
```

```go [sol1-Go]
func expandBinaryTree(root *TreeNode) *TreeNode {
	if root.Left != nil {
		root.Left = &TreeNode{-1, expandBinaryTree(root.Left), nil}
	}
	if root.Right != nil {
		root.Right = &TreeNode{-1, nil, expandBinaryTree(root.Right)}
	}
	return root
}
```
