---
title: LCP 44.开幕式焰火
slug: go-dfsha-xi-biao-by-endlesscheng-lqli
author: endlesscheng
date: 2021-09-25T10:05:46Z
---
# Go DFS+哈希表
 
> [原题 LCP 44.开幕式焰火](https://leetcode.cn/problems/sZ59z6)
```go
func numColor(root *TreeNode) int {
	color := map[int]bool{}
	var dfs func(*TreeNode)
	dfs = func(o *TreeNode) {
		if o == nil {
			return
		}
		color[o.Val] = true
		dfs(o.Left)
		dfs(o.Right)
	}
	dfs(root)
	return len(color)
}
```
