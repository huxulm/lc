---
title: LCP 39.无人机方阵
slug: jian-ji-xie-fa-yong-ha-xi-biao-tong-ji-c-7qzn
author: endlesscheng
date: 2021-09-11T09:37:46Z
---
# 用哈希表统计差异
 
> [原题 LCP 39.无人机方阵](https://leetcode.cn/problems/0jQkd0)
```go
func minimumSwitchingTimes(source, target [][]int) (ans int) {
	cnt := map[int]int{}
	for i, row := range source {
		for j, v := range row {
			cnt[v]++
			cnt[target[i][j]]--
		}
	}
	for _, c := range cnt {
		ans += abs(c)
	}
	return ans / 2
}

func abs(x int) int {
	if x < 0 {
		return -x
	}
	return x
}
```
