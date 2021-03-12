# [搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)

找到旋转数组的旋转点，即最小值，看target在数组的前半部分还是后半部分，再用二分查找。  
注意有可能不旋转，查找之前先判断第一个元素和最后一个元素的大小。  

*也可以直接在二分查找的循环中判断，mid左右是否有序（`nums[mid]>nums[left]`），看target在左在右*

```java
public int findMin(int[] nums) {
    int left=0,right=nums.length-1;
    while(left<right) {
        int mid=left+(right-left)/2;
        if(nums[mid]>nums[right]) {
            left=mid+1;
        } else {
            right=mid;
        }
    }
    return right;
}
public int search(int[] nums, int target) {
    int left=0,right=nums.length-1;
    if(nums[left]>nums[right]) {
        if(nums[left]<=target) {
            right=findMin(nums);
        }else if(nums[right]>=target) {
            left=findMin(nums);
        } else {
            return -1;
        }
    }
    while(left<=right) {
        int mid=left+(right-left)/2;
        if(nums[mid]==target) {
            return mid;
        } else if(nums[mid]<target) {
            left=mid+1;
        } else {
            right=mid-1;
        }
    }
    return -1;
}
```
