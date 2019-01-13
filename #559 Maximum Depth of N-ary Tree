# 559. Maximum Depth of N-ary Tree

## Description
Given a n-ary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

For example, given a ``3-ary`` tree:

![tree](.\pics\narytreeexample2.png)

We should return its max depth, which is 3.

**Note:**

1. The depth of the tree is at most ``1000``.
2. The total number of nodes is at most ``5000``.

## Solutions

真后悔当时数据结构没学好，一碰到树就懵逼。

```python
class Solution(object):
    def maxDepth(self, root):
        """
        :type root: Node
        :rtype: int
        """
        if root is None:
            return 0
        elif root.children == []:
            return 1
        else:
            height = [self.maxDepth(c) for c in root.children]
            return max(height) + 1
```

这是递归的解法。

```python
class Solution(object):
    def maxDepth(self, root):
        """
        :type root: Node
        :rtype: int
        """
        stack = []
        if root is not None:
            stack.append((1, root))
        depth = 0
        while stack != []:
            current_depth, root = stack.pop()
            if root is not None:
                depth = max(depth, current_depth)
                for c in root.children:
                    stack.append((current_depth + 1, c))
        return depth
```
这是用迭代的解法，用到了stack。