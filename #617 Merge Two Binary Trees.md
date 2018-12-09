## Description
Given two binary trees and imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not.

You need to merge them into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of new tree.

**Example 1:**
```
Input: 
	Tree 1                     Tree 2                  
          1                         2                             
         / \                       / \                            
        3   2                     1   3                        
       /                           \   \                      
      5                             4   7                  
Output: 
Merged tree:
	     3
	    / \
	   4   5
	  / \   \ 
	 5   4   7
```

**Note:**
The merging process must start from the root nodes of both trees.

## Solutions

```python
class Solution:
    def mergeTrees(self, t1, t2):
        """
        :type t1: TreeNode
        :type t2: TreeNode
        :rtype: TreeNode
        """
        if not t1:
            return t2
        elif not t2:
            return t1
        else:
            t1.val = t1.val + t2.val
            t1.left = self.mergeTrees(t1.left, t2.left)
            t1.right = self.mergeTrees(t1.right, t2.right)
            return t1
```
这题有两种解法，一种是递归，一种是迭代。上面的是递归方法。和绝大多数解法不同的是，上面的解法没有新建一棵新的树，而是将第二棵树加到第一棵树上。当其中一棵树为空值时将另一棵树的值作为t1的值，只有当两棵树同时非空的时候才会将两棵树的和作为t1的值。若是两棵树同时为空，则返回值也是空值。

```python
class Solution(object):
    def mergeTrees(self, t1, t2):
        """
        :type t1: TreeNode
        :type t2: TreeNode
        :rtype: TreeNode
        """
        if (t1 is None):
            return t2        
        if (t2 is None):
            return t1
        stack=[[t1,t2]]
        while (stack):
            root=stack.pop()
            if (root[0] is None or root[1] is None):
                continue
            root[0].val+=root[1].val
            if (root[0].left is None):
                root[0].left=root[1].left
            else:
                stack.append([root[0].left,root[1].left])
            if (root[0].right is None):
                root[0].right=root[1].right
            else:
                stack.append([root[0].right,root[1].right])
        return t1
```

这是这题的迭代解法。