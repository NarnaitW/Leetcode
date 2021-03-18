# [转变数组后最接近目标值的数组和](https://leetcode-cn.com/problems/sum-of-mutated-array-closest-to-target/)

根据提示，做出value和abs(sum-target)的关系图，可以知道该图是一条形似山谷的曲线，与山脉数组类似，所以只需要谷底的左边界即可。
时间复杂度*O(nlogn)*，空间复杂度*O(1)*

```java
public int total(int[] arr, int mid, int target) {
    int sum=0;
    for(int i=0;i<arr.length;i++) {
        sum += arr[i]>mid ? mid:arr[i];
    }
    return Math.abs(sum-target);
}
public int findBestValue(int[] arr, int target) {
    int l=0,r=target,ans=-1;
    while(l<=r) {
        int mid=l+(r-l)/2;
        if(total(arr, mid,target)>=total(arr, mid-1,target)) {
            r=mid-1;
            ans=mid-1;
        } else {
            l=mid+1;
        }
    }
    return ans;
}
```