---
title: LCP 61.气温变化趋势
slug: mo-ni-by-endlesscheng-mc05
author: endlesscheng
date: 2022-09-25T01:40:11Z
---
# 一些简化代码的技巧
 
> [原题 LCP 61.气温变化趋势](https://leetcode.cn/problems/6CE719)
```py [sol1-Python]
class Solution:
    def temperatureTrend(self, temperatureA: List[int], temperatureB: List[int]) -> int:
        ans = cnt = 0
        for (a1, b1), (a2, b2) in pairwise(zip(temperatureA, temperatureB)):
            if (a1 > a2) - (a1 < a2) == (b1 > b2) - (b1 < b2):
                cnt += 1
                ans = max(ans, cnt)
            else:
                cnt = 0
        return ans
```

```go [sol1-Go]
func temperatureTrend(a, b []int) (ans int) {
	start := 0
	for i := 1; i < len(a); i++ {
		if a[i] == a[i-1] != (b[i] == b[i-1]) || a[i] < a[i-1] != (b[i] < b[i-1]) {
			ans = max(ans, i-start-1)
			start = i
		}
	}
	return max(ans, len(a)-start-1)
}

func max(a, b int) int { if b > a { return b }; return a }
```
