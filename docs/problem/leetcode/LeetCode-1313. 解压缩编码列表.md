# LeetCode: 1313. 解压缩编码列表

[TOC]

## 1、题目描述

给你一个以行程长度编码压缩的整数列表 `nums` 。

考虑每相邻两个元素 `[a, b] = [nums[2*i], nums[2*i+1]]` （其中 `i >= 0` ），每一对都表示解压后有 `a` 个值为 `b` 的元素。

请你返回解压后的列表。

 

**示例：**

```
输入：nums = [1,2,3,4]
输出：[2,4,4,4]
```

**提示：**

-   $2 <= nums.length <= 100$
-   $nums.length % 2 == 0$
-   $1 <= nums[i] <= 100$



## 2、解题思路

-   直接展开即可



```python
class Solution:
    def decompressRLElist(self, nums: List[int]) -> List[int]:
        ans = []
        for index in range(0, len(nums), 2):
            ans.extend([nums[index+1] for _ in range(nums[index])])
        return ans

```

