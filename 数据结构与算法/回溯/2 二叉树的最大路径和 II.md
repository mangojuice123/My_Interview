- [题目](#题目)
- [Follow up](#follow-up)
- [测试用例](#测试用例)
- [题解](#题解)
- [复杂度](#复杂度)
- [公司](#公司)

</br></br>

# 题目
- [113. Path Sum II](https://leetcode.com/problems/path-sum-ii/description/)
> Given the root of a binary tree and an integer targetSum, return all root-to-leaf paths where the sum of the node values in the path equals targetSum. Each path should be returned as a list of the node values, not node references.

# Follow up
- [129. Sum Root to Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers/)
> 非递归使用层序遍历，原地修改结点的值。

# 测试用例

# 题解
1. 路径总和 II
```
class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
       curSum, res, path = 0, [], []
       self.backtracking(root, curSum, targetSum, res, path) 
       return res

    def backtracking(self, root, curSum, target, res, path):
        if root:
            curSum += root.val
            # 只有到达叶结点才可以添加到最终的答案中。
            if not root.left and not root.right:
                if curSum == target:
                    res.append(path + [root.val])
                    return
                    
            # 对于只有只有一个孩子的结点来说，会继续向有孩子的一边访问，另一边则会直接返回。
            # 对于相同父结点的孩子们来说，由上层传递来的消息都是一样的。
            self.backtracking(root.left, curSum, target, res, path + [root.val])
            self.backtracking(root.right, curSum, target, res, path + [root.val])
```
2. 求根结点到叶结点数字之和
```
class Solution:
    def __init__(self) -> None:
        self.res = 0

    def sumNumbers(self, root: Optional[TreeNode]) -> int:
        self.backtracking(root, 0)
        return self.res
        
    def backtracking(self, root, curSum):
        if root:
            curSum = curSum * 10 + root.val
            if not root.left and not root.right:
                self.res += curSum
                return

            self.backtracking(root.left, curSum)
            self.backtracking(root.right, curSum)
```

# 复杂度
- 时间复杂度：`O(n)`
- 空间复杂度：`O(h)`

# 公司