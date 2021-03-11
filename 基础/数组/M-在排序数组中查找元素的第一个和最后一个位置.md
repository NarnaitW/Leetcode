# [在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

两次二分查找，第一次找到target在数组的左边界，第二次找到target的右边界  
时间复杂度*O(logn)*

```java
public int[] searchRange(int[] nums, int target) {
    if(nums.length==0) {
        return new int[] {-1, -1};
    }
    int first=searchFirst(nums, target);
    if(first==-1) {
        return new int[] {-1, -1};
    }
    //执行到这里时，target一定在数组里，所以查找右边界，最后不用再次确认
    int last=searchLast(nums, target);
    return new int[] {first, last};
}

public int searchFirst(int[] nums, int target) {
    int left=0, right=nums.length-1;
    while(left<right) {
        int mid=left+(right-left)/2;
        if(target<=nums[mid]) {
            right=mid;
        } else {
            left=mid+1;
        }
    }
    if(nums[left]==target) {
        return left;
    } else {
        return -1;
    }
}

public int searchLast(int[] nums, int target) {
    int left=0, right=nums.length-1;
    while(left<right) {
        int mid=left+(right-left+1)/2;
        if(target>=nums[mid]) {
            left=mid;
        } else {
            right=mid-1;
        }
    }
    return left;
}
```
