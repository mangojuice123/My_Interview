- [题目](#题目)
- [Follow up](#follow-up)
- [测试用例](#测试用例)
- [题解](#题解)
- [复杂度](#复杂度)
- [公司](#公司)

</br></br>

# 题目
- [470. Implement Rand10() Using Rand7()](https://leetcode.com/problems/implement-rand10-using-rand7/description/)
> Given the API rand7() that generates a uniform random integer in the range [1, 7], write a function rand10() that generates a uniform random integer in the range [1, 10]. You can only call the API rand7(), and you shouldn't call any other API. Please do not use a language's built-in random API.

# Follow up
- `randP()`，有 P 的概率生成 0，1 - P 的概率生成 1，求 `randN()`。
    - [生成 `rand2()`](https://www.nowcoder.com/questionTerminal/248553ad24e64d8a922482c7c29c4aa0)：a = 0, b = 1 概率为 `P * (1 - P)`；a = 1，b = 0 概率为 `(1 - P) * P`，得到 `rand2()`。
    - 生成 `rand4()`，`rand16()`：`rand4()` = rand2() * 2 + rand2；`rand16()` = rand4() * 4 + rand4()。
        - rand4() * 4 = [0,4,8,12]
        - rand4() = [0,1,2,3]
        - 任意的一个组合覆盖了相应的区间，比如 rand4() * 4 = 0，那么下一个 rand4() 覆盖了 [0,1,2,3] 这个区间。
    - 生成 `randN()`（N 是某个数的平方），再进行拒绝策略即可。
# 测试用例

# 题解
- [构造古典概率模型](https://leetcode-cn.com/problems/implement-rand10-using-rand7/solution/mo-neng-gou-zao-fa-du-li-sui-ji-shi-jian-9xpz/)
```
class Solution:
    def rand10(self):
        """
        :rtype: int
        """

        first, second = 7, 7
        # 使用 [1,6] 的奇偶性来构造出 2 种结果。
        while first > 6:        
            first = rand7()

        # 使用 [1,5] 构造出 5 种结果。
        while second > 5:
            second = rand7()

        # 映射到 [1,10] 这个区间中。
        if first % 2 == 0:
            return second + 5
        else:
            return second
```

# 复杂度
- 时间复杂度：`O()`
- 空间复杂度：`O(1)`

# 公司
- 2021-10 百度