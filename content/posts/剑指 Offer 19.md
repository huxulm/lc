---
title: 剑指 Offer 19.正则表达式匹配
slug: go-yi-xing-by-endlesscheng-7x8c
author: endlesscheng
date: 2021-07-14T03:17:06Z
---
# Go 一行
 
> [原题 剑指 Offer 19.正则表达式匹配](https://leetcode.cn/problems/zheng-ze-biao-da-shi-pi-pei-lcof)
```go
func isMatch(s, p string) bool {
	return regexp.MustCompile("^" + p + "$").MatchString(s)
}
```
