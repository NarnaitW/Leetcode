# [搜索插入位置](https://leetcode-cn.com/problems/search-insert-position/)

## 二分查找
在有序数组中，设置左右指针，判断左右指针的中位数与目标数的大小关系。  
若目标数>中位数，则中位数设为左指针；若目标数<中位数，则中位数设为右指针。  
不断循环，直到左指针>=右指针。  
二分查找中需要注意的是循环终止条件、mid的整数性和返回值。  
伪代码：
```python
def binarySearch(self, nums: List[int], target: int):
    left = 0, right = len(nums)-1
    while(left < right):
        mid = (left + right) / 2     //注意保证mid为整数
        if(nums[mid] == target):
            break
        elif(nums[mid] > target):
            right = mid
        else:
            left = mid
```
