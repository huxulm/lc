---
title: LCS 02.完成一半题目
slug: tan-xin-by-endlesscheng-kz1d
author: endlesscheng
date: 2021-06-19T07:51:13Z
---
# 贪心
 
> [原文链接](https://leetcode.cn/problems/WqXACV/solution/tan-xin-by-endlesscheng-kz1d)
统计每个数的个数，按个数从大到小排序，然后依次选择直到选择个数超过 $n/2$。

```go
func halfQuestions(a []int) (ans int) {
	cnt := [1001]int{}
	for _, v := range a {
		cnt[v]++
	}
	sort.Ints(cnt[:])
	for i, n := 1000, len(a)/2; n > 0; i-- {
		ans++
		n -= cnt[i]
	}
	return
}
```
