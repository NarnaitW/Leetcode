# [寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)

旋转数组中前一部分的元素都大于后一部分元素  
用二分查找，比较mid元素值与right元素值的大小，若mid元素值较大，则最小值在mid之后；反之，在mid之前。

```java
public int findMin(int[] nums) {
    int left=0, right=nums.length-1;
    while(left<right) {
        int mid=left+(right-left)/2;
        if(nums[mid]>nums[right]) {
           left=mid+1;
        } else {
           right=mid;
        }
    }
    return nums[right];
}
```
