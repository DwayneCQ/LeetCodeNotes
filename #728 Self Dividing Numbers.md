## Description

A *self-dividing number* is a number that is divisible by every digit it contains.

For example, 128 is a self-dividing number because ``128 % 1 == 0``, ``128 % 2 == 0``, and ``128 % 8 == 0``.

Also, a self-dividing number is not allowed to contain the digit zero.

Given a lower and upper number bound, output a list of every possible self dividing number, including the bounds if possible.

**Example 1:**
```
Input: 
left = 1, right = 22
Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15, 22]
```

**Note:**

- The boundaries of each input argument are ``1 <= left <= right <= 10000``.

## Solutions

```python
class Solution(object):
    def selfDividingNumbers(self, left, right):
        """
        :type left: int
        :type right: int
        :rtype: List[int]
        """
        selfdiv = []
        for i in range(left, right + 1):
            ls = str(i)
            flag = True
            for j in ls:
                if j == '0' or i % int(j) != 0:
                    flag = False
                    break 
            if flag == True:
                selfdiv.append(i)
        return selfdiv
```

我自己的解法又是思路很直接很简单。感觉实在太蠢了。

```python
class Solution(object):
    def selfDividingNumbers(self, left, right):
        """
        :type left: int
        :type right: int
        :rtype: List[int]
        """
        result = []
        for i in range(left, right+1):
            n = i
            while n:
                r = n % 10
                if r == 0 or i % r:
                    break
                wn = n / 10
            else:
                result.append(i)
        return result
```
在discuss中看到一个思路非常巧妙的解法。但是不知道为什么自己在本地运行的时候没有返回值。

```python
class Solution(object):
    def selfDividingNumbers(self, left, right):
        def self_dividing(n):
            for d in str(n):
                if d == '0' or n % int(d) > 0:
                    return False
            return True
        """
        Alternate implementation of self_dividing:
        def self_dividing(n):
            x = n
            while x > 0:
                x, d = divmod(x, 10)
                if d == 0 or n % d > 0:
                    return False
            return True
        """
        ans = []
        for n in range(left, right + 1):
            if self_dividing(n):
                ans.append(n)
        return ans #Equals filter(self_dividing, range(left, right+1))
```
官方给出的解法跟我的思路一样。