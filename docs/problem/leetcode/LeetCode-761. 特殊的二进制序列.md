# LeetCode: 761. 特殊的二进制序列

[TOC]

## 1、题目描述

特殊的二进制序列是具有以下两个性质的二进制序列：

`0` 的数量与 `1` 的数量相等。
二进制序列的每一个前缀码中 `1` 的数量要大于等于 `0` 的数量。
给定一个特殊的二进制序列 `S`，以字符串形式表示。定义一个操作 为首先选择 `S` 的两个连续且非空的特殊的子串，然后将它们交换。（两个子串为连续的当且仅当第一个子串的最后一个字符恰好为第二个子串的第一个字符的前一个字符。)

在任意次数的操作之后，交换后的字符串按照字典序排列的最大的结果是什么？

**示例 1:**

```
输入: S = "11011000"
输出: "11100100"
解释:
将子串 "10" （在S[1]出现） 和 "1100" （在S[3]出现）进行交换。
这是在进行若干次操作后按字典序排列最大的结果。
```


**说明:**

- `S 的长度不超过 50。`
- `S 保证为一个满足上述定义的特殊 的二进制序列。`



## 2、解题思路

- 首先分析一下，如果是满足题目要求的字符串，必然起始字符是`"1"`，结束字符是`"0"`
  - 首先将字符串进行分割，分割成满足条件的子串
  - 然后针对每个子串，去掉首尾字符后递归
  - 最后针对已经内部排好序的子串进行排序，并且链接返回

```
例如：11011000
	1、首先进行子串分割，得到：
		[11011000]
	2、然后去掉首尾字符，得到 101100，递归处理
	3、分割子串 101100，得到
		[10,1100]
		分别继续递归处理，返回值依旧是上面本身
		然后字典序排序，连接返回 
		110010
	4、添加上首尾的1，0
		11100100
	5、由于数组中只有一个元素，排序连接直接返回本身
```



```python
class Solution:
    def makeLargestSpecial(self, S: str) -> str:
        
        if not S:
            return ""

        length = len(S)
        pos = 0
        res = S
        count_ones = 0

        # 子串分割
        pre_substring = []

        pre = pos
        for i in range(pos, length):
            if res[i] == "1":
                count_ones += 1
            elif res[i] == "0":
                count_ones -= 1
            if count_ones == 0:
                pre_substring.append("1" + self.makeLargestSpecial(res[pre + 1:i]) + "0")
                pre = i + 1

        return "".join(sorted(pre_substring, reverse=True))
```

