- [题目](#题目)
- [Follow up](#follow-up)
- [测试用例](#测试用例)
- [题解](#题解)
- [复杂度](#复杂度)
- [公司](#公司)

</br></br>

# 题目
- [93. Restore IP Addresses](https://leetcode.com/problems/restore-ip-addresses/description/)
> A valid IP address consists of exactly four integers separated by single dots. Each integer is between 0 and 255 (inclusive) and cannot have leading zeros.

# Follow up

# 测试用例

# 题解
```
class Solution:
    def restoreIpAddresses(self, s: str) -> List[str]:
        res = []
        self.backtracking(s, [], 0, res)
        return res
    
    def backtracking(self, s, IP, start, res):
        n = len(s)
        # 当已经有了一个完整的 4 段地址，且到达 s 的末尾，添加到答案列表中。
        if len(IP) == 4 and start == n:
            res.append('.'.join(IP))
            return

        # 4 段 IP 已经被分配完，但是此时还没有到达底部，不能成为一个答案。
        if len(IP) > 4:
            return

        # 如果 IP 还没有 4 段，但是到达了 s 尾部，不会进入循环。
        # min(start + 3, n) 是优化，避免无意义的循环。
        for i in range(start, min(start + 3, n)):
            # 除去前导 0。
            if s[start] == '0' and i > start:
                continue
            # 因为 s[start: i + 1] 长度最多为 3，所以前两位一定可以递归，第三位必须小于 255 才能进行递归。
            if int(s[start: i + 1]) <= 255:
                self.backtracking(s, IP + [s[start: i + 1]], i + 1, res)
```

# 复杂度
- 时间复杂度：`O()`
- 空间复杂度：`O()`

# 公司
- 2021-9 百度
- 2021-8 米哈游
- 2021-8 字节跳动
- 2021-7 华为
- 2021-4 快手