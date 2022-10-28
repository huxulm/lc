---
title: LCS 01.下载插件
slug: yi-xing-xie-fa-by-endlesscheng-p1gx
author: endlesscheng
date: 2021-06-19T07:49:00Z
---
# 一行写法
 
> [原文链接](https://leetcode.cn/problems/Ju9Xwi/solution/yi-xing-xie-fa-by-endlesscheng-p1gx)
```go
func leastMinutes(n int) int {
	return bits.Len(uint(n-1)) + 1
}
```
