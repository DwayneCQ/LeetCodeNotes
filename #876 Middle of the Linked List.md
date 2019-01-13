# 876. Middle of the Linked List

## Description

Given a non-empty, singly linked list with ``head`` node head, return a middle node of linked list.

If there are two middle nodes, return the second middle node.

**Example 1:(())
```
Input: [1,2,3,4,5]
Output: Node 3 from this list (Serialization: [3,4,5])
The returned node has value 3.  (The judge's serialization of this node is [3,4,5]).
Note that we returned a ListNode object ans, such that:
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, and ans.next.next.next = NULL.
```

**Example 2:**

```
Input: [1,2,3,4,5,6]
Output: Node 4 from this list (Serialization: [4,5,6])
Since the list has two middle nodes with values 3 and 4, we return the second one.
```

**Note:**

The number of nodes in the given list will be between ``1`` and ``100``.

## Solutinos

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def middleNode(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        ls = []
        if head.next == None:
            return [head.val]
        else:
            while head:
                ls.append(head.val)
                head = head.next
            return ls[int(len(ls)/2):]
```

这个初步看上去我就只想到用列表将这个序列储存然后输出后一半。但是看了官方解法中提供的快慢指针方法，发现还是有更好的解决办法的。

```python
class Solution(object):
    def middleNode(self, head):
        slow = fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        return slow
```

慢指针每次步幅为1，快指针为2.当快指针到达序列尾部时，慢指针刚好到中间。所以直接返回慢指针即可。