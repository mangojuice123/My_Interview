- [题目](#题目)
- [Follow up](#follow-up)
- [测试用例](#测试用例)
- [题解](#题解)
- [复杂度](#复杂度)
- [公司](#公司)

</br></br>

# 题目
- [240. Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/)

# Follow up

# 测试用例

# 题解
```
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        m, n = len(matrix), len(matrix[0])
        # 从右上角开始搜索，类似搜索二叉树。
        row, col = 0, n - 1
        
        while row < m and col >= 0:
            if matrix[row][col] == target:
                return True
            elif matrix[row][col] > target:
                col -= 1
            else:
                row += 1
        return False
```

# 复杂度
- 时间复杂度：`O(m + n)`
- 空间复杂度：`O(1)`

# 公司
- 2021-9 滴滴