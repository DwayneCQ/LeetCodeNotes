## Description
There is a robot starting at position (0, 0), the origin, on a 2D plane. Given a sequence of its moves, judge if this robot **ends up at (0, 0)** after it completes its moves.

The move sequence is represented by a string, and the character moves[i] represents its ith move. Valid moves are R (right), L (left), U (up), and D (down). If the robot returns to the origin after it finishes all of its moves, return true. Otherwise, return false.

**Note:** The way that the robot is "facing" is irrelevant. "R" will always make the robot move to the right once, "L" will always make it move left, etc. Also, assume that the magnitude of the robot's movement is the same for each move.

**Example 1:**

```
Input: "UD"
Output: true 
Explanation: The robot moves up once, and then down once. All moves have the same magnitude, so it ended up at the origin where it started. Therefore, we return true.
```

**Example 2:**
```
Input: "LL"
Output: false
Explanation: The robot moves left twice. It ends up two "moves" to the left of the origin. We return false because it is not at the origin at the end of its moves.
```

## Solutions

```python
class Solution:
    def judgeCircle(self, moves):
        """
        :type moves: str
        :rtype: bool
        """
        x = {'U':0, 'D':0, 'L':-1, 'R':1}
        y = {'U':1, 'D':-1,'L':0,'R':0}
        position = [0, 0]
        for i in moves:
            position[0] += x[i]
            position[1] += y[i]
        if position[0] == 0 and position[1] == 0:
            return True
        else:
            return False
```

这是我一开始写的代码，用坐标简单的模拟了机器人的移动。
Disscuss中有一个一行实现。

```python
class Solution(object):
    def judgeCircle(self, moves):
        l = [0] * 128 # Allocate enough space to index 'UDLR' into the array. Could also be an array of size 4 and then index appropriately in the for loop below.
        for move in moves:
            l[ord(move)] += 1
		# L == R and U == D for you to return to the origin point
        return l[ord('L')] == l[ord('R')] and l[ord('U')] == l[ord('D')]
```

受到启发，写了另一个：

```python
class Solution:
    def judgeCircle(self, moves):
        """
        :type moves: str
        :rtype: bool
        """
        count_U = moves.count('U')
        count_D = moves.count('D')
        count_L = moves.count('L')
        count_R = moves.count('R')
        return count_U == count_D and count_L == count_R
```

运行速度极快，有一次超过了100%的pythoners。
其实这个也可以写成一行。

```python
class Solution:
    def judgeCircle(self, moves):
        """
        :type moves: str
        :rtype: bool
        """
        return moves.count('U') == moves.count('D') and moves.count('L') == moves.count('R')
```

但是经过测试没有上一个快，也是之前一个未知的问题。
官方给出的解法没有什么亮点。

```python
class Solution(object):
    def judgeCircle(self, moves):
        x = y = 0
        for move in moves:
            if move == 'U': y -= 1
            elif move == 'D': y += 1
            elif move == 'L': x -= 1
            elif move == 'R': x += 1

        return x == y == 0
```
