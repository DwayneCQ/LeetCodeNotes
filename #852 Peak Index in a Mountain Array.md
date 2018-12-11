## Description
Let's call an array ``A`` a mountain if the following properties hold:

- ``A.length >= 3``

- There exists some ``0 < i < A.length - 1`` such that ``A[0] < A[1] < ... A[i-1] < A[i] > A[i+1] > ... > A[A.length - 1]``
Given an array that is definitely a mountain, return any ``i`` such that ``A[0] < A[1] < ... A[i-1] < A[i] > A[i+1] > ... > A[A.length - 1]``.

**Example 1:**
```
Input: [0,1,0]
Output: 1
```

**Example 2:**
```
Input: [0,2,1,0]
Output: 1
```

**Note:**

1. ``3 <= A.length <= 10000``

2. ``0 <= A[i] <= 10^6``

3. A is a mountain, as defined above.

## Solutions

```python
class Solution(object):
    def peakIndexInMountainArray(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        return A.index(max(A))
```
这题出的不好。一开始我以为是检测这个列表是不是符合mountain的定义，结果认真一看是返回mountain的序号。这样就没意思了。唯一的点就是在如何寻找这个最大值。我直接用的python内置的方法``max()``。

```python
class Solution(object):
    def peakIndexInMountainArray(self, A):
        lo, hi = 0, len(A) - 1
        while lo < hi:
            mi = (lo + hi) / 2
            if A[mi] < A[mi + 1]:
                lo = mi + 1
            else:
                hi = mi
        return lo
```

官方给出了二分查找的解法，但是在列表长度不长的情况下速度上并没有区别。