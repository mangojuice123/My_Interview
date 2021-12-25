- [List Comprehension](#list-comprehension)
- [sort](#sort)


</br></br>


# List Comprehension
- 无论生成几维数据，只能使用 **List Comprehension**，禁止使用 `[0] * n` 形式。
```
dp = [0 for i in range(n + 1)]

o = [Object() for i in range(n + 1)]

matrix = [
    [Object() for j in range(n + 1)]
    for i in range(m + 1)
]
```

# sort
- sort 的 key 参数可以直接用 key 进行比较，也可以利用 `cmp_to_key` 转换为比较函数。
```
from functools import cmp_to_key
# 当 compare 返回是正数时 交换两元素（交换后 y 在前）
def compare(x, y):
    return y - x

res = sorted(res, key=cmp_to_key(compare))
```