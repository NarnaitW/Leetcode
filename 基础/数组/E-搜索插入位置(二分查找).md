# [搜索插入位置](https://leetcode-cn.com/problems/search-insert-position/)

简单的二分查找

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
