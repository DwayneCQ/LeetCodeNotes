## Description
Given a string S that only contains "I" (increase) or "D" (decrease), let ``N = S.length``.

Return any permutation ``A`` of ``[0, 1, ..., N]`` such that for all ``i = 0, ..., N-1``:

- If ``S[i] == "I"``, then ``A[i] < A[i+1]``

- If ``S[i] == "D"``, then ``A[i] > A[i+1]``

**Example 1:**

```
Input: "IDID"
Output: [0,4,1,3,2]
```

**Example 2:**

```
Input: "III"
Output: [0,1,2,3]
```

**Example 3:**

```
Input: "DDI"
Output: [3,2,0,1]
```

**Note:**

1. ``1 <= S.length <= 10000``

2. ``S`` only contains characters ``"I"`` or ``"D"``.

## Solutions

```python
class Solution(object):
    def diStringMatch(self, S):
        """
        :type S: str
        :rtype: List[int]
        """
        low, high = 0, len(S)
        ls = []
        for c in S:
            if c == 'I':
                ls.append(low)
                low += 1
            elif c == 'D':
                ls.append(high)
                high -= 1
        return ls + [high]     
```
这个算法官方称它为‘Ad-Hoc’算法。其实讲的是一个贪婪的思想。题目的意思是按照字符串给出的规则进行排序，只要符合两个规则都是正确的。也就是，这道题的正确输出其实不唯一。那么我们选取最容易解决的方法进行解题。

贪婪的思想就是只考虑当前情况下的最优解而不去考虑全局的最优解。在这题中也就是，当看到``'I'``的时候就在前一位选取当前候选数字中最小的数字，给他足够的空间去增大；看到``'D'``的时候，就选取最大的数字。

当完成对字符串的遍历后，将所有数字中还剩余的一个数字添加到输出列表的最后即使所求的列表。此时，``low``和``high``两个值是相等的，无论最后在返回是返回的是哪一个都是正确答案。

这一题一开始确实是没有什么思路，偷偷看了discuss之后才有的思路。确实还是太年轻了。