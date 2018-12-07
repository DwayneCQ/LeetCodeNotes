## Description

Given an array ``A`` of non-negative integers, return an array consisting of all the even elements of ``A``, followed by all the odd elements of ``A``.

You may return any answer array that satisfies this condition.

**Example1:**

```
Input: [3,1,2,4]
Output: [2,4,3,1]
The outputs [4,2,3,1], [2,4,1,3], and [4,2,1,3] would also be accepted.
```

**Note:**

- ``1 <= A.length <= 5000``
- ``0 <= A[i] <= 5000``

## Solutions
```python
class Solution(object):
    def sortArrayByParity(self, A):
        """
        :type A: List[int]
        :rtype: List[int]
        """
        even = []
        odd = []
        for i in A:
            if i % 2 == 0:
                even.append(i)
            else:
                odd.append(i)
        return even+odd
```
由于我是从难度最低的开始做，所以前面的题还真是简单。不过官方的解法又比我简洁很多。

```python
class Solution(object):
    def sortArrayByParity(self, A):
        A.sort(key = lambda x: x % 2)
        return A
```
官方的解法使用了``sort()``，通过一个``lambda``作为筛选条件。
下面贴出``sort()``的函数介绍
```
sort(*, key=None, reverse=False)
This method sorts the list in place, using only < comparisons between items. Exceptions are not suppressed - if any comparison operations fail, the entire sort operation will fail (and the list will likely be left in a partially modified state).  

sort() accepts two arguments that can only be passed by keyword (keyword-only arguments):

key specifies a function of one argument that is used to extract a comparison key from each list element (for example, key=str.lower). The key corresponding to each item in the list is calculated once and then used for the entire sorting process. The default value of None means that list items are sorted directly without calculating a separate key value.

The functools.cmp_to_key() utility is available to convert a 2.x style cmp function to a key function.

reverse is a boolean value. If set to True, then the list elements are sorted as if each comparison were reversed.

This method modifies the sequence in place for economy of space when sorting a large sequence. To remind users that it operates by side effect, it does not return the sorted sequence (use sorted() to explicitly request a new sorted list instance).

The sort() method is guaranteed to be stable. A sort is stable if it guarantees not to change the relative order of elements that compare equal — this is helpful for sorting in multiple passes (for example, sort by department, then by salary grade).

CPython implementation detail: While a list is being sorted, the effect of attempting to mutate, or even inspect, the list is undefined. The C implementation of Python makes the list appear empty for the duration, and raises ValueError if it can detect that the list has been mutated during a sort.
```

