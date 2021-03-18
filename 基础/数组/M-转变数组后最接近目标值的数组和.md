# [ת���������ӽ�Ŀ��ֵ�������](https://leetcode-cn.com/problems/sum-of-mutated-array-closest-to-target/)

������ʾ������value��abs(sum-target)�Ĺ�ϵͼ������֪����ͼ��һ������ɽ�ȵ����ߣ���ɽ���������ƣ�����ֻ��Ҫ�ȵ׵���߽缴�ɡ�
ʱ�临�Ӷ�*O(nlogn)*���ռ临�Ӷ�*O(1)*

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