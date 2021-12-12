- [题目](#题目)
- [Follow up](#follow-up)
- [测试用例](#测试用例)
- [题解](#题解)
- [复杂度](#复杂度)
- [公司](#公司)

</br></br>

# 题目
- [8. String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)
> Implement the myAtoi(string s) function, which converts a string to a 32-bit signed integer (similar to C/C++'s atoi function).

# Follow up
- [7. Reverse Integer](https://leetcode.com/problems/reverse-integer/)

# 测试用例

# 题解
1. atoi()
```
class Solution:
    def myAtoi(self, s: str) -> int:
        # 位移符号的优先级很低，需要加括号。
        INT_MAX = (1 << 31) - 1
        INT_MIN = - (1 << 31)
        pre = INT_MAX // 10
        res = 0
        flag = 1
        i = 0
        n = len(s)
        if n < 1:
            return 0
        
        # i < n 防止溢出。
        # 空格处理。
        while i < n and s[i] == ' ':
            i += 1
        
        # 正负号处理。
        if i < n and s[i] == '-':
            flag = -1
        if i < n and (s[i] == '-' or s[i] == '+'):
            i += 1

        # 字符串处理。
        while i < n and s[i].isdigit():
            number = ord(s[i]) - ord('0')

            # 提前判断是否会溢出。
            # 2 的 31 次方 = 2147483648
            if res > pre or (res == pre and number > 7):
                return INT_MAX if flag > 0 else INT_MIN

            res = res * 10 + number            
            i += 1

        return res if flag > 0 else -res
```

2. Reverse Integer
```
class Solution:
    def reverse(self, x: int) -> int:
        res = 0

        if x < 0:
            symbol = -1
            # 将负数变为正数处理。
            x = -x
        else:
            symbol = 1

        while x:
            res = res * 10 + x % 10
            x //= 10
        
        return 0 if res > (1 << 31) else res * symbol
```

# 复杂度
- 时间复杂度：`O(n)`
- 空间复杂度：`O(1)`

# 公司
- 2021-9 百度
- 2021-8 腾讯