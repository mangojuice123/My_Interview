- [题目](#题目)
- [Follow up](#follow-up)
- [测试用例](#测试用例)
- [题解](#题解)
- [复杂度](#复杂度)
- [公司](#公司)

</br></br>

# 题目
- [468. Validate IP Address](https://leetcode.com/problems/validate-ip-address/description/)
> Given a string queryIP, return "IPv4" if IP is a valid IPv4 address, "IPv6" if IP is a valid IPv6 address or "Neither" if IP is not a correct IP of any type.

# Follow up

# 测试用例

# 题解
```
class Solution:
    def validIPAddress(self, queryIP: str) -> str:
        import string
        flag = True
        ipv4 = queryIP.split('.')
        if len(ipv4) == 4:
            for x in ipv4:
                if x == '' or (x[0] == '0' and len(x) != 1) or not x.isdigit() or int(x) > 255:
                    flag = False
                    break
            if flag:
                return 'IPv4'

        ipv6 = queryIP.split(':')
        if len(ipv6) == 8:
            for x in ipv6:
                # 注意如何判断一个字符串是否是 16 进制的写法。
                if x == '' or len(x) > 4 or not all(c in string.hexdigits for c in x):
                    flag = False
                    break
            if flag:
                return 'IPv6'

        return 'Neither'
```

# 复杂度
- 时间复杂度：`O(n)`
- 空间复杂度：`O(1)`

# 公司
- 2021-8 美团