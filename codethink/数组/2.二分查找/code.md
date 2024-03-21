# 二分查找

给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。

示例 1:
>输入: nums = [-1,0,3,5,9,12], target = 9     
>输出: 4       
>解释: 9 出现在 nums 中并且下标为 4    

示例 2:

>输入: nums = [-1,0,3,5,9,12], target = 2     
输出: -1        
解释: 2 不存在 nums 中因此返回 -1   

提示：

- 你可以假设 nums 中的所有元素是不重复的。
- n 将在 [1, 10000]之间。
- nums 的每个元素都将在 [-9999, 9999]之间。

## 思路
#### 直接思路
首先想到直接暴力遍历求解
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        for i, v in enumerate(nums):
            if v == target:
                return i
        return -1
```
需要遍历完全部数组，需要$O(n)$的时间复杂度；
使用的额外内存空间与输入大小$n$无关，因此空间复杂度$O(1)$.

提交后消耗：
>时间：43ms（47.94%）; 空间：17.32MB（79.06%）

#### 二分查找

由于给定的数组是升序，且只查找一个确定的数值，去中间数值`mid`，若`target == mid` 则直接返回下标，否则根据`target`与`mid`的相对大小判断具体位置。

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        right = 0
        left = len(nums)
        mid = (right + left) // 2
        while (right < left):
            if target > nums[mid]:
                right = mid + 1
                mid = (right + left) // 2
                continue
            elif target == nums[mid]:
                return mid
            else:
                left = mid
                mid = (right + left) // 2
                continue
        return -1
```

- **难点**
主要在与如何确定每一次遍历后，`mid`应该确定的范围和`right`与`left`在下一次遍历中应该被确定的值。
由实际意义可知，`right`指向被遍历数组中的第一个元素，而`left`指向的是被遍历数组中的最后一个元素的后一个元素。`[right, left)`间的元素是我们确定的要查找的元素范围，由于`mid`是已经查找过的元素，所以在改变`right`时，使用`right = mid + 1`，以略过以查找过的元素。
而改变`left`时，被`left`指向的元素是在需要查找的元素的后一个元素，因此直接使用`left = mid`即可

复杂度分析：
二分法相当与把整个遍历过程看作一棵二叉树，我们只沿着可能有`target`的分支前进，因此时间复杂度为$O(\log{n})$
只使用了固定的空间，因此空间复杂度为$O(1)$

提交后的消耗：
>时间：39ms（71%）， 空间：17.31MB（82%）