# 867. Transpose Matrix

## Description

Given a matrix ``A``, return the transpose of ``A``.

The transpose of a matrix is the matrix flipped over it's main diagonal, switching the row and column indices of the matrix.

**Example 1:**

```
Input: [[1,2,3],[4,5,6],[7,8,9]]
Output: [[1,4,7],[2,5,8],[3,6,9]]
```

**Example 2:**

```
Input: [[1,2,3],[4,5,6]]
Output: [[1,4],[2,5],[3,6]]
```

**Note:**

1. 1 <= A.length <= 1000
2. 1 <= A[0].length <= 1000

## Solutions

```python
class Solution(object):
    def transpose(self, A):
        """
        :type A: List[List[int]]
        :rtype: List[List[int]]
        """
        re = []
        for i in range(len(A[0])):
            tmp = []
            for j in range(len(A)):
                tmp.append(A[j][i])
            re.append(tmp)
        return re
```

这个解答用了很简单的方法，用了两个循环。可以用行内循环进行简化。

```python
class Solution(object):
    def transpose(self, A):
        """
        :type A: List[List[int]]
        :rtype: List[List[int]]
        """
        output = []
        for i in range(len(A[0])):
            output.append([A[j][i] for j in range(len(A))])
        return output
```

我在评论区看到了一种神奇做法。

```python
class Solution(object):
    def transpose(self, A):
        return list(zip(*A))
```

这个是用*将A中的元素当作位置参数传入，然后用zip将相同位置的数组合成一个列表，最终将类型转化为列表。实在是高啊。