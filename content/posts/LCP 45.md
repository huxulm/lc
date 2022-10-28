---
title: LCP 45.自行车炫技赛场
slug: zhuang-tai-she-ji-bfs-by-endlesscheng-nf0j
author: endlesscheng
date: 2021-09-25T10:07:14Z
---
# 状态设计+BFS 
 
> [原文链接](https://leetcode.cn/problems/kplEvH/solution/zhuang-tai-she-ji-bfs-by-endlesscheng-nf0j)
根据题目的数据范围，选手到任意位置的速度至多为 $101$，那么可以用 $(x,y,\textit{speed})$ 表示状态，从起点 $(\textit{position}[0],\textit{position}[1],1)$ 开始跑 BFS。

BFS 结束后，如果 $(x,y,1)$ 被访问过，那么将 $(x,y)$ 计入答案中。注意起点不能计入答案。

```go
var dir4 = []struct{ x, y int }{{-1, 0}, {1, 0}, {0, -1}, {0, 1}}

func bicycleYard(position []int, terrain, obstacle [][]int) (ans [][]int) {
	n, m := len(terrain), len(terrain[0])
	vis := make([][][102]bool, n)
	for i := range vis {
		vis[i] = make([][102]bool, m)
	}

	sx, sy := position[0], position[1]
	vis[sx][sy][1] = true
	type pair struct{ x, y, speed int }
	q := []pair{{sx, sy, 1}}
	for len(q) > 0 {
		p := q[0]
		q = q[1:]
		x, y, speed := p.x, p.y, p.speed
		for _, d := range dir4 {
			if xx, yy := x+d.x, y+d.y; 0 <= xx && xx < n && 0 <= yy && yy < m {
				s := speed + terrain[x][y] - terrain[xx][yy] - obstacle[xx][yy]
				if s > 0 && !vis[xx][yy][s] {
					vis[xx][yy][s] = true
					q = append(q, pair{xx, yy, s})
				}
			}
		}
	}

	vis[sx][sy][1] = false // 起点不计入答案
	for i, row := range vis {
		for j, b := range row {
			if b[1] {
				ans = append(ans, []int{i, j})
			}
		}
	}
	return
}
```
