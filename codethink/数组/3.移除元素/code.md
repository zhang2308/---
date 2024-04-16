# 移除元素

给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并原地修改输入数组。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

示例 1: 给定 nums = [3,2,2,3], val = 3, 函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。 你不需要考虑数组中超出新长度后面的元素。

示例 2: 给定 nums = [0,1,2,2,3,0,4,2], val = 2, 函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。

## 思路

直接遍历该数组，将目标值跳过，并将后面的元素赋值到前面空的位置上即可。

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        next_val = 0
        length = len(nums)
        i = 0
        while i < length:
            while next_val < length and nums[next_val] == val:
                next_val += 1
            if next_val >= length:
                return i
            nums[i] = nums[next_val]
            next_val += 1
            i += 1
        return i
```

完全需要完全遍历一次数组，不需要使用额外空间，因此时间复杂度： $ O(n) $ , 空间复杂度 $ O(1) $ .
提交后消耗：
>时间：45ms（8%）； 空间：16.45MB（29%）
**难点**
主要在于python中for循环的使用。
由于 ` for i in range(length) ` 语句在 ` length == 0 ` 时，无法确定 ` i ` 的值，导致程序出现错误
这里直接改用while循环避免出现无法确定的情况。