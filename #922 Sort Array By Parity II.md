# #922 Sort Array By Parity II

## Description

Given an array ``A`` of non-negative integers, half of the integers in A are odd, and half of the integers are even.

Sort the array so that whenever ``A[i]`` is odd, ``i`` is odd; and whenever ``A[i]`` is even, ``i`` is even.

You may return any answer array that satisfies this condition.

**Example 1:**
```
Input: [4,2,5,7]
Output: [4,5,2,7]
Explanation: [4,7,2,5], [2,5,4,7], [2,7,4,5] would also have been accepted.
```

**Note:**

1. ``2 <= A.length <= 20000``

2. ``A.length % 2 == 0``

3. ``0 <= A[i] <= 1000``

## Solutions

```python
class Solution(object):
    def sortArrayByParityII(self, A):
        """
        :type A: List[int]
        :rtype: List[int]
        """
        x = []
        y = []
        for i in range(len(A)):
            if i % 2 == 0:
                if A[i] % 2 != 0:
                    x.append(i)
                else:
                    continue
            if i % 2 != 0:
                if A[i] % 2 == 0:
                    y.append(i)
                else:
                    continue
        for j in range(len(x)):
            A[x[j]], A[y[j]] = A[y[j]], A[x[j]]
        return A
```

这道题要求将奇数放在奇数位，偶数放在偶数位。只要是存在位置与数值不匹配的情况，那么一定是奇数和偶数成对错误。所以只要将错误的位匹配上并交换位置即可。


```python
class Solution(object):
    def sortArrayByParityII(self, A):
        j = 1
        for i in xrange(0, len(A), 2):
            if A[i] % 2:
                while A[j] % 2:
                    j += 2
                A[i], A[j] = A[j], A[i]
        return A
```

顺着上面的思路延伸出去，可以发现，只要将奇数位或者偶数位确定，则另一半就可以确定。上面的代码就使用了这一思路。

```python
class Solution(object):
    def sortArrayByParityII(self, A):
        """
        :type A: List[int]
        :rtype: List[int]
        """
        result = [0 for i in range(len(A))]
        even = 0
        odd = 1
        for i in A:
            if (not i % 2):
                result[even] = i
                even+= 2
            else:
                result[odd] = i
                odd+= 2
        return result
```

上面提供了另一种思路，不是交换错误的位置，而是将将奇数填入奇数位，偶数填入偶数位。虽然看起来更加复杂，但是其实时间复杂度是一样的。