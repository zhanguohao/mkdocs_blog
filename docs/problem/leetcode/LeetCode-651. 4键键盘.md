# LeetCode: 651. 4键键盘

[TOC]

## 1、题目描述

假设你有一个特殊的键盘包含下面的按键：

-   `Key 1: (A)`：在屏幕上打印一个 `'A'`。
-   `Key 2: (Ctrl-A)`：选中整个屏幕。
-   `Key 3: (Ctrl-C)`：复制选中区域到缓冲区。
-   `Key 4: (Ctrl-V)`：将缓冲区内容输出到上次输入的结束位置，并显示在屏幕上。



现在，你只可以按键 `N` 次（使用上述四种按键），请问屏幕上最多可以显示几个 `'A'`呢？

**样例** 1:

```
输入: N = 3
输出: 3
解释: 
我们最多可以在屏幕上显示三个'A'通过如下顺序按键：
A, A, A
```

**样例 2:**

```
输入: N = 7
输出: 9
解释: 
我们最多可以在屏幕上显示九个'A'通过如下顺序按键：
A, A, A, Ctrl A, Ctrl C, Ctrl V, Ctrl V
```

**注释:**

-   $1 <= N <= 50$
-   结果不会超过 `32` 位有符号整数范围。



## 2、解题思路

-   动态规划
-   对每个操作考虑两种情况
    -   前面操作加一
    -   或者是从前面第`j`个开始，进行一次全选，一次复制，多次粘贴的操作`（j>=2）`



```python
class Solution:
    def maxA(self, N: int) -> int:
        dp = [0] * (N + 1)

        for i in range(1, N + 1):
            # 第i次操作为key1
            dp[i] = dp[i - 1] + 1
            # 第i次操作为key4
            for j in range(2, i - 1):
                dp[i] = max(dp[i], dp[j - 1] * (i - j))
        return dp[-1]
```

