- [切片](#切片)
- [匿名函数](#匿名函数)


</br></br>


# 切片
- 使用 make 来生成二维定长切片。
```
    m, n := 3, 4
    dp := make([][]int, m)          // 确定二维切片为 3 行。
    for i := range dp {             // 遍历切片，只关心索引的情况。
            dp[i] = make([]int, n)  // 确定每一行 4 列。
    }
```

# 匿名函数
- go 中函数是一等公民，可以将函数赋值给变量或作为参数传递。
```
    get := func(i int) int {
        if i == -1 || i == n {
            return math.MinInt64
        }
        return nums[i]
```