# 有序数组的平方

给你一个按 非递减顺序 排序的整数数组 nums，返回 每个数字的平方 组成的新数组，要求也按 非递减顺序 排序。

示例 1：

>输入：nums = [-4,-1,0,3,10]
>输出：[0,1,9,16,100]
>解释：平方后，数组变为 [16,1,0,9,100]，排序后，数组变为 [0,1,9,16,100]

示例 2：

>输入：nums = [-7,-3,2,3,11]
>输出：[4,9,9,49,121]

## 思路

### 直接思路

对每个元素取平方，然后对数组进行排序

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        for i in range(len(nums)):
            nums[i] = nums[i] ** 2
        nums.sort()
        return nums
```

时间复杂度： $ O(n\log{n}) $ ; 空间复杂度： $ O(1) $.
提交后消耗：
>时间：83.55%， 空间：98.34%

### 进阶

进阶要求：算法时间复杂度为 $ O(n) $.
直接使用双指针从两头开始遍历，选取绝对值更大的数进行平方，并放入新数组末尾。

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        a = 0
        b = len(nums) - 1
        res = [0 for i in range(len(nums))]
        index = len(res) - 1
        while a < b:
            if abs(nums[a]) > abs(nums[b]):
                res[index] = nums[a] ** 2
                a += 1
            else:
                res[index] = nums[b] ** 2
                b -= 1
            index -= 1
        if index != -1:
            res[index] = nums[a] ** 2
        return res

```

时间复杂度： $ O(n) $ ; 空间复杂度： $ O(n) $.
提交后消耗：
>时间：25.66%， 空间：58.64%

由于脚本语言原因，该算法比直接使用内置sort算法要慢一些。

**难点**
主要在于双指针遍历时，在最后一个元素的处理上。若有奇数个元素，由于程序原因，可能最后一个元素不会被计算。故加上一行若结果数组最后一个元素没有被写入，则手动写入最后一个元素。
