- [partition 的实现](#partition-的实现)
- [特殊输入测试](#特殊输入测试)
- [功能性测试](#功能性测试)

# partition 的实现
- 小于主元的部分 $~$|$~$ 等于主元的部分 $~$|$~$ 大于主元的部分
- 小于主元的部分 | 等于主元的部分 | 大于主元的部分
```
def partition(self, nums, left, right):
    import random
    pivot = random.randint(left, right)
    nums[left], nums[pivot] = nums[pivot], nums[left]
    
    pivot = nums[left]
    while left < right:
        while left < right and nums[right] > pivot:
            right -= 1
        nums[left] = nums[right]
        # 注意这里的符号是 <= 
        while left < right and nums[left] <= pivot:
            left += 1
        nums[right] = nums[left]
        
    nums[left] = pivot
    return left
```

# 特殊输入测试
- `nums = []`
- `nums = [1]`

# 功能性测试