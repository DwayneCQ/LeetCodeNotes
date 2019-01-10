# 509. Fibonacci Number

## Description

The **Fibonacci numbers**, commonly denoted ``F(n)`` form a sequence, called the **Fibonacci sequence**, such that each number is the sum of the two preceding ones, starting from ``0`` and ``1``. That is,

```
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), for N > 1.
Given N, calculate F(N).
```

**Example 1:**

```
Input: 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.
```

**Example 2:**

```
Input: 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.
```

**Example 3:**

```
Input: 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
```

**Note:**

0 ≤ ``N`` ≤ 30.

## Solutions

```python
class Solution(object):
    def fib(self, N):
        """
        :type N: int
        :rtype: int
        """
        if N == 0:
            return 0
        elif N == 1:
            return 1
        return self.fib(N-1)+self.fib(N-2)
```

这题用递归写就比较简单。通常来说，斐波那契数列在课本上就是用来当成递归的典型案例。在讨论中我看到一种更为简洁的办法。

```python
class Solution(object):
    def fib(self, N):
        """
        :type N: int
        :rtype: int
        """
        if N <= 1:
            return N
        return self.fib(N-1)+self.fib(N-2)
```

不得不说这个小哥是真的有想法。里面返回的N是表示序号而不是数列的值，但是前两位序号和值又恰好相等，所以这样表示虽然有的时候会产生误解，但是确实是相当简洁。

```python
class Solution(object):
    def fib(self, N):
        """
        :type N: int
        :rtype: int
        """
        if N == 0:
            return 0
        elif N == 1:
            return 1
        else:
            re = [0, 1]
            for i in range(2, N+1):
                re.append(re[i-1] + re[i-2])
        return re[-1]
```

可以用列表将整个斐波那契数列储存，最后返回列表的最后一个值。

```python
class Solution(object):
    def fib(self, N):
        """
        :type N: int
        :rtype: int
        """
        if N == 0:
            return 0
        elif N == 1:
            return 1
        else:
            tmp1 = 0
            tmp2 = 1
            for i in range(2,N+1):
                re = tmp1 + tmp2
                tmp1 = tmp2
                tmp2 = re
        return re
```

也可以用两个变量保存前面的两个数列。这样做虽然看起来非常原始简陋，但是速度是最快的。

