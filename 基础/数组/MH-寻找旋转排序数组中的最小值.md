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
# [寻找旋转排序数组中的最小值2](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)

此题为上面题目的延伸，若数组中包含重复元素  
依然用二分查找，循环内部，若mid元素值分别大于、小于right元素值，情况不变。  
如果mid元素值等于right元素值，此时并不能确定最小值在mid左边还是右边，我们把right左移一位，继续判断。  
二分查找时间复杂度为 *O(logn)* ，最坏情况是数组中元素全部相等，此时算法时间复杂度为 *O(n)*
```java
public int findMin(int[] nums) {
    int left=0, right=nums.length-1;
    while(left<right) {
        int mid=left+(right-left)/2;
        if(nums[mid]>nums[right]) {
            left=mid+1;
        } else if(nums[mid]<nums[right]) {
            right=mid;
        } else {
            right-=1;
        }
    }
    return nums[right];
}
```
