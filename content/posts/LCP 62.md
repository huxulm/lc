---
title: LCP 62.交通枢纽
slug: an-zhao-ti-yi-mo-ni-by-endlesscheng-41jb
author: endlesscheng
date: 2022-09-25T01:31:28Z
---
# 按题意模拟
 
> [原文链接](https://leetcode.cn/problems/D9PW8w/solution/an-zhao-ti-yi-mo-ni-by-endlesscheng-41jb)
```py [sol1-Python]
class Solution:
    def transportationHub(self, path: List[List[int]]) -> int:
        nodes = set()
        out_deg = Counter()
        in_deg = Counter()
        for x, y in path:
            nodes.add(x)
            nodes.add(y)
            out_deg[x] += 1
            in_deg[y] += 1
        for x in nodes:
            if out_deg[x] == 0 and in_deg[x] == len(nodes) - 1:
                return x
        return -1
```
 
```go [sol1-Go]
func transportationHub(path [][]int) int {
	nodes := map[int]struct{}{}
	outDeg := map[int]int{}
	inDeg := map[int]int{}
	for _, p := range path {
		x, y := p[0], p[1]
		nodes[x] = struct{}{}
		nodes[y] = struct{}{}
		outDeg[x]++
		inDeg[y]++
	}
	for x := range nodes {
		if outDeg[x] == 0 && inDeg[x] == len(nodes)-1 {
			return x
		}
	}
	return -1
}
```
