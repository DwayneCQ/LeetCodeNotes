# #561 Array Partition I

## Description

Given an array of **2n** integers, your task is to group these integers into n pairs of integer, say (a1, b1), (a2, b2), ..., (an, bn) which makes sum of min(ai, bi) for all i from 1 to n as large as possible.

**Example 1:**
```
Input: [1,4,3,2]

Output: 4
Explanation: n is 2, and the maximum sum of pairs is 4 = min(1, 2) + min(3, 4).
```

**Note:**

1. n is a positive integer, which is in the range of [1, 10000].

2. All the integers in the array will be in the range of [-10000, 10000].

## Solutions
```python
class Solution(object):
    def arrayPairSum(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        nums = sorted(nums)
        return sum(nums[0:len(nums):2])
```
这题的意思是将长度为2n的列表分成n对，使每一对最小值的和最大。这样的分法，其实将相邻的两个数结成一对就可以了。
所以在解答的时候只需要将其排序，并且输出偶数位上的数字的和即可。
习惯性看了一下讨论区，发现一模一样的思路有更简洁的解法。
```python
class Solution(object):
    def arrayPairSum(self, A):
        return sum(sorted(A)[::2])
```
还是比较年轻，没有意识到这些简化的方法。之后要注意一下如何简化代码。
