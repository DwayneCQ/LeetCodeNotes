## Description
The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Given two integers ``x`` and ``y``, calculate the Hamming distance.

**Note:**
0 ≤ ``x``, ``y ``< 231.

**Example:**

```
Input: x = 1, y = 4

Output: 2

Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑

The above arrows point to positions where the corresponding bits are different.
```

## Solutions

```python
class Solution(object):
    def hammingDistance(self, x, y):
        """
        :type x: int
        :type y: int
        :rtype: int
        """
        return bin(x^y).count('1')
```
这题的思路是将两个数异或之后计算异或后的数中1的个数。
其中的要点就是：``bin()``、``hex()``等函数返回的形式是字符串，也就能够用``count()``方法来计算字符串中某个元素的个数。知道了这个要点这题就迎刃而解了。