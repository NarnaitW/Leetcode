# [寻找峰值](https://leetcode-cn.com/problems/find-peak-element/)

返回任一峰值均可，常规的二分查找

## Java
```java
public int findPeakElement(int[] nums) {
    int l=0,r=nums.length-1;
    while(l<r) {
        int m=l+(r-l)/2;
        if(nums[m]>nums[m+1]) {
            r=m;
        } else {
            l=m+1;
        }
    }
    return l;
}
```
