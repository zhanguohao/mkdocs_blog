# LeetCode: 807. 保持城市天际线

[TOC]

## 1、题目描述

在二维数组`grid`中，`grid[i][j]`代表位于某处的建筑物的高度。 我们被允许增加任何数量（不同建筑物的数量可能不同）的建筑物的高度。 高度 0 也被认为是建筑物。

最后，从新数组的所有四个方向（即顶部，底部，左侧和右侧）观看的“天际线”必须与原始数组的天际线相同。 城市的天际线是从远处观看时，由所有建筑物形成的矩形的外部轮廓。 请看下面的例子。

建筑物高度可以增加的最大总和是多少？

**例子：**

```
输入： grid = [[3,0,8,4],[2,4,5,7],[9,2,6,3],[0,3,1,0]]
输出： 35
解释： 
The grid is:
[ [3, 0, 8, 4], 
  [2, 4, 5, 7],
  [9, 2, 6, 3],
  [0, 3, 1, 0] ]

从数组竖直方向（即顶部，底部）看“天际线”是：[9, 4, 8, 7]
从水平水平方向（即左侧，右侧）看“天际线”是：[8, 7, 9, 3]

在不影响天际线的情况下对建筑物进行增高后，新数组如下：

gridNew = [ [8, 4, 8, 7],
            [7, 4, 7, 7],
            [9, 4, 8, 7],
            [3, 3, 3, 3] ]

```

**说明:**

- `1 < grid.length = grid[0].length <= 50。`

- `grid[i][j]` 的高度范围是： `[0, 100]`。 

- 一座建筑物占据一个`grid[i][j]`：换言之，它们是 `1 x 1 x grid[i][j]` 的长方体。

## 2、解题思路

- 先判断出天际线的高度
- 然后同一个坐标的最大高度不能超过横纵天际线的最小值



```python
class Solution:
    def maxIncreaseKeepingSkyline(self, grid: List[List[int]]) -> int:
        row = len(grid)
        col = len(grid[0])

        line_row = [float('-inf') for _ in range(row)]
        line_col = [float('-inf') for _ in range(col)]

        for i in range(row):
            for j in range(col):
                line_row[i] = max(line_row[i], grid[i][j])
                line_col[j] = max(line_col[j], grid[i][j])
        res = 0
        print(line_row)
        print(line_col)
        for i in range(row):
            for j in range(col):
                res += min(line_row[i], line_col[j]) - grid[i][j]
        return res
```

