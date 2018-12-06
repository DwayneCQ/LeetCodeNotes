## Description （Eazy）

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the same element twice.

**Example:**
```
Given nums = [2, 7, 11, 15], target = 9,  

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## Solutions

```python
class Solution(object):
    def twoSum(self, nums, target):
        if len(nums) <= 1:
            return False
        buff_dict = {}
        for i in range(len(nums)):
            if nums[i] in buff_dict:
                return [buff_dict[nums[i]], i]
            else:
                buff_dict[target - nums[i]] = i
```

这个是我在disscuss里找到的一个python版本的解法，时间复杂度为O(n)。由于这是我做的第一题，还不熟悉，我自己的解法被我弄丢了。具体思路差不多，只是方法比较复杂。


这个解法的思路就是将整个数组遍历一遍，将每一个数和目标值的差存入一个字典中作为键，数的序号作为值。同时判断字典中是不是存在跟当前数一样的数。若字典中存在和当前数相同的数，则直接返回两个数对应的序号；若不存在，则将差存入字典。

---

官方有三种解法：

### Solution 1

```java
public int[] twoSum(int[] nums, int target) {
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[j] == target - nums[i]) {
                return new int[] { i, j };
            }
        }
    }
    throw new IllegalArgumentException("No two sum solution");
}
```

第一种就是简单粗暴的用两个循环全部遍历一遍，如果找到加起来是目标值的值，就返回两个序号。
时间复杂度为 $O(n^2)$， 时间复杂度为 $O(1)$
### Solution 2
```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        map.put(nums[i], i);
    }
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement) && map.get(complement) != i) {
            return new int[] { i, map.get(complement) };
        }
    }
    throw new IllegalArgumentException("No two sum solution");
}
```
这个解法先用一个循环将数值存在一个hash table中，在第二个循环中查找每个数的差值是否在hash table中。用空间换时间，空间复杂度从 $O(1)$ 变为 $O(n)$ 但是时间复杂度减小到 $O(n)$。

### Solution 3
```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[] { map.get(complement), i };
        }
        map.put(nums[i], i);
    }
    throw new IllegalArgumentException("No two sum solution");
}
```
这个其实就是开头用Python实现的算法。