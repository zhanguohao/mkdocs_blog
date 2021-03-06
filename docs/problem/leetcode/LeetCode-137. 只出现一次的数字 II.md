# LeetCode: 137. 只出现一次的数字 II

[TOC]



## 1、题目描述



给定一个**非空**整数数组，除了某个元素只出现一次以外，其余每个元素均出现了三次。找出那个只出现了一次的元素。

**说明：**

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

**示例 1:**

```
输入: [2,2,3,2]
输出: 3
```

**示例 2:**

```
输入: [0,1,0,1,0,1,99]
输出: 99
```



## 2、解题思路

​	在前面，做过只出现一次的数字，当时其他所有的数字出现的都是2次，于是直接用异或就出来了

​	在这里，因为出现的是3次，不能直接使用异或来做，不过还是可以考虑位运算

​	我们发现，如果某一位，比如第0位，不考虑只出现1次的那个数，出现1的次数是x，出现0的次数是y

​	那么3x+3y = n-1

​	也就是说，如果在某一位上，出现3次1，我们就可以将它清零

​	考虑用3个变量，保存出现3次1的次数，2次1的次数，1次1的次数，遇到一个数，我们就更新一下

​	这样最后剩下的那个只出现1次的，就是想要找的数

​	举个例子

```
输入: [2,2,3,2]
一开始，three=0,two=0,one=0
然后,取到数字2，找出那几个出现了3次，需要用two来判断
three = 2 & two
然后，我们先从two中，去掉出现了3次的1，然后利用one更新出现了两次的1
```

```python
class Solution:
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        one = 0
        two = 0
        three = 0

        for i in nums:
            # 更新出现了3次的1
            three = two & i
            # 在出现了两次的1的基础上，去掉出现了3次的1，数字中也去掉
            two = two & ~three
            i = i & ~three
            # 更新出现了两次的1
            two |= one & i
            # 更新出现了一次的1
            one ^= i
        return one
```
