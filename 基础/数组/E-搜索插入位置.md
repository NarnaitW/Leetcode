# [搜索插入位置](https://leetcode-cn.com/problems/search-insert-position/)

简单的二分查找，相当于搜索一个数，while后面的边界条件有等号，if相等就返回索引  
最后的返回值考虑最后一次循环：  
当left==right时，mid=left，此时target只可能在mid及其前后位置，若nums[mid]<target，应返回mid+1即left；
若nums[mid]>target，应插入mid位置，mid及后面的数依次后移，此时right=mid-1，返回left=mid
## Java
```java
public int searchInsert(int[] nums, int target) {
    int left=0,right=nums.length-1,mid=0;
    while(left<=right) {
        mid=left+(right-left)/2;
        if(nums[mid]==target)
            return mid;
        else if(nums[mid]<target)
            left=mid+1;
        else if(nums[mid]>target)
            right=mid-1;
    }
    return left;
}
```
## Python
```python
def searchInsert(self, nums: List[int], target: int) -> int:
    left,right=0,len(nums)-1
    while left<=right:
        mid=left+int((right-left)/2)
        if nums[mid]==target:
            return mid
        elif nums[mid]<target:
            left=mid+1
        else:
            right=mid-1
    return left
```
