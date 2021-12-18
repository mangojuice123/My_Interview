- [生成列表元素](#生成列表元素)


</br></br>


# 生成列表元素
- 无论几维数据，只能使用 **List Comprehension**，禁止使用 `[0] * n` 形式。
```
dp = [0 for i in range(n + 1)]

o = [Object() for i in range(n + 1)]

matrix = [
    [Object() for j in range(n + 1)]
    for i in range(m + 1)
]
```