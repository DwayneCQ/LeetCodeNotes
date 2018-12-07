## Description

Implement function ToLowerCase() that has a string parameter str, and returns the same string in lowercase.

## Solutions
```python
class Solution(object):
    def toLowerCase(self, str):
        """
        :type str: str
        :rtype: str
        """
        str = str.lower()
        return str
```

这个又是太简单以至于没有官方解法。
其实这个可以只用一行代码就完成也就是

```python
class Solution(object):
    def toLowerCase(self, str):
        """
        :type str: str
        :rtype: str
        """
        return str.lower()
```

但是很奇怪这样还更慢一点，目前还不知道为什么，以后知道了再来补充。