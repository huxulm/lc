---
title: LCP 42.玩具套圈
slug: er-fen-bao-li-mei-ju-by-endlesscheng-vezb
author: endlesscheng
date: 2021-09-11T09:40:25Z
---
# 排序二分+暴力枚举
 
> [原题 LCP 42.玩具套圈](https://leetcode.cn/problems/vFjcfV)
注意到半径很小，我们可以枚举每个玩具，并暴力枚举该玩具**周围**是否有可以套住该玩具的圈。

具体来说，将 $\textit{circles}$ 排序后，将横坐标相同的圈分为一组。对每个玩具，可以套住该玩具的圈，在横坐标上，必然满足圈的最右端点不小于玩具的最右端点，且圈的最左端点不大于玩具的最左端点。对于纵坐标，我们只需要找最接近玩具纵坐标的上下两个圈。这样我们就可以二分出圈的横坐标的范围，对每个横坐标上的圈二分纵坐标最接近玩具纵坐标的圈。

```go
func circleGame(toys [][]int, circles [][]int, r0 int) (ans int) {
	sort.Slice(circles, func(i, j int) bool { a, b := circles[i], circles[j]; return a[0] < b[0] || a[0] == b[0] && a[1] < b[1] })

	// 将横坐标相同的圈分为一组
	type pair struct{ x int; ys []int }
	a, y := []pair{}, -1
	for _, p := range circles {
		if len(a) == 0 || p[0] > a[len(a)-1].x {
			a = append(a, pair{p[0], []int{p[1]}})
			y = -1
		} else if p[1] > y { // 去重
			a[len(a)-1].ys = append(a[len(a)-1].ys, p[1])
			y = p[1]
		}
	}

	for _, t := range toys {
		x, y, r := t[0], t[1], t[2]
		if r > r0 {
			continue
		}
		i := sort.Search(len(a), func(i int) bool { return a[i].x+r0 >= x+r })
		for ; i < len(a) && a[i].x-r0 <= x-r; i++ {
			cx, ys := a[i].x, a[i].ys
			j := sort.SearchInts(ys, y)
			if j < len(ys) {
				if cy := ys[j]; (x-cx)*(x-cx)+(y-cy)*(y-cy) <= (r0-r)*(r0-r) {
					ans++
					break
				}
			}
			if j > 0 {
				if cy := ys[j-1]; (x-cx)*(x-cx)+(y-cy)*(y-cy) <= (r0-r)*(r0-r) {
					ans++
					break
				}
			}
		}
	}
	return
}
```
