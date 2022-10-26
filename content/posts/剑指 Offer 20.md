---
title: 剑指 Offer 20.表示数值的字符串
slug: golang-hua-shi-guo-ti-by-endlesscheng-g3hm
author: endlesscheng
date: 2021-01-15T13:59:46Z
---
# Golang 花式过题
 
> [原题 剑指 Offer 20.表示数值的字符串](https://leetcode.cn/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof)
这题标准解法是手撸一个 DFA，或者用正则匹配。

另一种类似正则匹配的方法是用 `big.Float` 来读入这个字符串，但是由于它无法支持超过 `int32` 范围的指数，需要稍微改造一下，把指数部分提出来读入。

通过额外读入一个字符串的方式来判断是否**恰好**读完了该字符串。

此外，由于题目仅允许十进制的表达形式，在其他进制中含有的 `'b' 'o' 'p' 'x'` 是不允许的。

```go
func isNumber(s string) bool {
    s = strings.ToLower(strings.TrimSpace(s))
    if strings.ContainsAny(s, " bopx") {
        return false
    }
    if i := strings.IndexAny(s, "e"); i >= 0 {
        n1, _ := fmt.Sscan(s[:i], new(big.Float), new(string))
        n2, _ := fmt.Sscanf(s[i+1:], "%d%s", new(big.Int), new(string)) // %d 强制以十进制方式读入
        return n1 == 1 && n2 == 1
    }
    n, _ := fmt.Sscan(s, new(big.Float), new(string))
    return n == 1
}
```
