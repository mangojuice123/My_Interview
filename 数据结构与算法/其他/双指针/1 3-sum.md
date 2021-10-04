# 题解
```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums = sorted(nums)
        ans = []
        n = len(nums)

        for i in range(n - 2):
            if nums[i] > 0:
                break
            if i > 0 and nums[i] == nums[i - 1]:
                continue

            left = i + 1
            right = n - 1
            target = 0 - nums[i]
            while left < right:
                temp = nums[left] + nums[right]
                if temp == target:
                    ans.append([nums[i], nums[left], nums[right]])
                    while left < right and nums[left] == nums[left + 1]:
                        left += 1
                    left += 1
                    while left < right and nums[right] == nums[right - 1]:
                        right -= 1
                    right -= 1
                elif temp < target:
                    left += 1
                elif temp > target:
                    right -= 1
            
        return ans
```

# 复杂度
- 时间：`O(n^2)`
- 空间：`O(1)`