# LeetCode: 312. 戳气球

[TOC]

## 1、题目描述

有 `n` 个气球，编号为`0` 到 `n-1`，每个气球上都标有一个数字，这些数字存在数组 `nums` 中。

现在要求你戳破所有的气球。每当你戳破一个气球 i 时，你可以获得 `nums[left] * nums[i] * nums[right]` 个硬币。 这里的 `left` 和 `right` 代表和 `i` 相邻的两个气球的序号。注意当你戳破了气球 `i` 后，气球 `left` 和气球 `right` 就变成了相邻的气球。

求所能获得硬币的最大数量。

**说明:**

- `你可以假设 nums[-1] = nums[n] = 1，但注意它们不是真实存在的所以并不能被戳破。`
- `0 ≤ n ≤ 500, 0 ≤ nums[i] ≤ 100`

**示例:**

```
输入: [3,1,5,8]
输出: 167 
解释: nums = [3,1,5,8] --> [3,5,8] -->   [3,8]   -->  [8]  --> []
     coins =  3*1*5      +  3*5*8    +  1*3*8      + 1*8*1   = 167
```



## 2、解题思路

- 使用动态规划
- 状态转换方程

```
dp[i][j] ： 表示从i到j中间的所有气球都戳破了所得到的最大的硬币（不包含i，j）

mid: 表示i到j中最后一个被戳破的气球

因为在(i,j)中间，mid的取值有多个，所以需要遍历
dp[i][j] = max( nums[i]*nums[mid]*nums[j] + dp[i][mid]+ dp[mid][j] )

因为更长的区间的值需要短的区间的值，所以先将短的区间的值计算出来

```



```python
class Solution:
    def maxCoins(self, nums: List[int]) -> int:
        
        temp = [1] + nums[:] + [1]
        length = len(temp)

        dp = [[0 for _ in range(length)] for _ in range(length)]

        for len_judge in range(2, length):
            for i in range(length - len_judge):

                j = i + len_judge
                for mid in range(i + 1, j):
                    dp[i][j] = max(dp[i][j], temp[i] * temp[mid] * temp[j] + dp[i][mid] + dp[mid][j])

        return dp[0][length - 1]
```

