# 590. N-ary Tree Postorder Traversal

## Description

Given an n-ary tree, return the postorder traversal of its nodes' values.

For example, given a ```3-ary``` tree:

![pic](./pics/#590.png)

Return its postorder traversal as: ``[5,6,3,2,4,1]``.

**Note:**

Recursive solution is trivial, could you do it iteratively?

## Solutions

```python
"""
# Definition for a Node.
class Node(object):
    def __init__(self, val, children):
        self.val = val
        self.children = children
"""
class Solution(object):
    def postorder(self, root):
        """
        :type root: Node
        :rtype: List[int]
        """
        if root == None:
            return []
        stack, ls = [root, ], []
        while stack:
            root = stack.pop()
            if root is not None:
                ls.append(root.val)
            stack.extend(root.children)
        return ls[::-1]
```
这题跟上面的一题一样，只不过一个是前序遍历一个是后序遍历。