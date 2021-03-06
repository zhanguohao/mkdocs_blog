# LeetCode: 1209. 删除字符串中的所有相邻重复项 II

[TOC]

## 1、题目描述

给你一个字符串 s，「k 倍重复项删除操作」将会从 s 中选择 k 个相邻且相等的字母，并删除它们，使被删去的字符串的左侧和右侧连在一起。

你需要对 s 重复进行无限次这样的删除操作，直到无法继续为止。

在执行完所有删除操作后，返回最终得到的字符串。

本题答案保证唯一。

 

**示例 1：**

```
输入：s = "abcd", k = 2
输出："abcd"
解释：没有要删除的内容。
```


**示例 2：**

```
输入：s = "deeedbbcccbdaa", k = 3
输出："aa"
解释： 
先删除 "eee" 和 "ccc"，得到 "ddbbbdaa"
再删除 "bbb"，得到 "dddaa"
最后删除 "ddd"，得到 "aa"
```

**示例 3：**

```
输入：s = "pbbcggttciiippooaais", k = 2
输出："ps"
```

**提示：**

-   `1 <= s.length <= 10^5`
-   `2 <= k <= 10^4`
-   `s 中只含有小写英文字母。`



## 2、解题思路

-   递归法
-   直到每次找不到需要删除的元素为止



```python
from itertools import groupby


class Solution:
    def removeDuplicates(self, s: str, k: int) -> str:
        if len(s) < k:
            return s

        res = []
        flag = False
        for key, g in groupby(s):
            length = len(list(g))
            if length >= k:
                flag = True
            res.extend([key] * (length % k))

        if not flag:
            return "".join(res)
        else:
            return self.removeDuplicates("".join(res), k)
```




-   使用栈
-   栈中每一个元素保存两部分：字符与字符数量
-   一旦数量等于k，出栈



```python
class Solution:
    def removeDuplicates(self, s: str, k: int) -> str:
        stack = []

        for ch in s:
            if not stack:
                stack.append([ch, 1])
            else:
                if stack[-1][0] == ch:
                    stack[-1][1] += 1
                else:
                    stack.append([ch, 1])

            if stack[-1][1] == k:
                stack.pop()


        return "".join([x * num for x, num in stack])
```


