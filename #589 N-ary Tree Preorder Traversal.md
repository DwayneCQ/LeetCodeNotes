# 589. N-ary Tree Preorder Traversal

## Description
Given an n-ary tree, return the preorder traversal of its nodes' values.

For example, given a ``3-ary`` tree:
![pic](./pics/narytreeexample.png)
Return its preorder traversal as: ``[1,3,5,6,2,4]``.

**Note:**

Recursive solution is trivial, could you do it iteratively?

## Solutions

```python
class Solution(object):
    def preorder(self, root):
        """
        :type root: Node
        :rtype: List[int]
        """
        if root is None:
            return []
        stack, output = [root, ], []
        while stack:
            root = stack.pop()
            output.append(root.val)
            stack.extend(root.children[::-1])
        return output
```

在题目中要求最好用迭代的方式解题，我对树还是理解不够深，偷偷看了官方解法。上面的解法关键在于``extend()``函数。
``extend()`` 和 ``append()`` 的区别主要在于extend将一个序列加入列表中，而append将对象加入列表。因此，在while循环中，使用了栈的概念，将节点的子节点们倒序push入栈中，然后在下一个循环中将最后一个节点pop出，直到stack为空。
disscuss中有提到在倒序push入栈的时候，用``reverse()``会更快一些。经过我的测试，好像并没有快，可能是因为多次提交整体速度会慢一些的原因。

```python
class Solution(object):
    def preorder(self, root):
        ret, q = [], root and [root]
        while q:
            node = q.pop()
            ret.append(node.val)
            q += [child for child in node.children[::-1] if child]
        return ret
```

这个是discuss中一个非常简洁的迭代解法。其中精髓在于第一行，非常简洁的完成了对root节点是否为空的判断。后续我觉得相对没有官方解法的美观。

由于我对递归的理解不是很深，所以我又看了递归的解法。

```python
class Solution(object):
    def preorder(self, root):
        """
        :type root: Node
        :rtype: List[int]
        """
        if not root:
            return []
        output = [root.val]
        for child in root.children:
            output.extend(self.preorder(child))
        return output
```
