---
title: LCP 66.最小展台数量
slug: python-yi-xing-by-endlesscheng-6s44
author: endlesscheng
date: 2022-10-07T23:35:17Z
---
# Python 一行
 
> [原题 LCP 66.最小展台数量](https://leetcode.cn/problems/600YaG)
`Counter` 本质上表示的是一个多重集，直接用 `|` 就可以计算并集了。

```py [sol1-Python3]
class Solution:
    def minNumBooths(self, demand: List[str]) -> int:
        return sum(reduce(or_, map(Counter, demand)).values())
```

```go [sol1-Go]
func minNumBooths(demand []string) (ans int) {
	maxCnt := [26]int{}
	for _, s := range demand {
		cnt := [26]int{}
		for _, b := range s {
			cnt[b-'a']++
		}
		for i, c := range cnt {
			maxCnt[i] = max(maxCnt[i], c)
		}
	}
	for _, c := range maxCnt {
		ans += c
	}
	return
}

func max(a, b int) int { if b > a { return b }; return a }
```

