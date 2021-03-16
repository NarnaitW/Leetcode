# [山脉数组中查找目标值](https://leetcode-cn.com/problems/find-in-mountain-array/)

先用二分查找找到山脉数组的最大值即峰顶，再看峰顶左边是否存在target，若没有则搜索右边  
搜索左边和搜索右边可用同一个函数binarySearch，由于左边是升序，右边是降序，所以需要添加一个参数flag来确定数组是升序降序  
如果是降序，则把数组所有数乘上-1，使其变为升序数组，查找-target

```java
public int binarySearch(int target, MountainArray mountainArr, int left, int right, boolean flag) {
    if(!flag) {
        target*=-1;
    }
    while(left<=right) {
        int mid=left+(right-left)/2;
        int cur=mountainArr.get(mid)*(flag ? 1:-1);
        if(cur==target) {
            return mid;
        } else if(cur<target) {
            left=mid+1;
        } else {
            right=mid-1;
        }
    }
    return -1;
}
public int findInMountainArray(int target, MountainArray mountainArr) {
    //先找到峰值下标
    int l=0,r=mountainArr.length()-1;
    while(l<r) {
        int mid=l+(r-l)/2;
        if(mountainArr.get(mid)<mountainArr.get(mid-1)) {
            r=mid;
        } else {
            l=mid+1;
        }
    }
    int peak=l;
    //搜索左边
    int index=binarySearch(target, mountainArr, 0, peak, true);
    if(index!=-1) {
        return index;
    } else {    //搜索右边
        return binarySearch(target, mountainArr, peak, mountainArr.length()-1, false);
    }
}
```
