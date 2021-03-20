# [�ָ���������ֵ](https://leetcode-cn.com/problems/split-array-largest-sum/)

ʹ�ö��ֲ��ҵ�˼·��  
Ҫ�ҵ�m��������͵����ֵ�������Ͻ������������ĺͣ��½���������Ԫ�ص����ֵ��  
���ǿ��Կ��ǣ�����������͵����ֵ�������ܰ������Ϊ�����ǿ����������顣  
����ָ����������Ŀ>m��˵�����������ֵ̫С����֮�������������Ŀ<=m����Ҫ�ҵ�Ŀ��ֵӦ�ø�С��
ʱ�临�Ӷ�*O(nlog(sum-maxn))*���ռ临�Ӷ�*O(1)*

```java
public int splitNumber(int[] nums, int maxsum) {
		int sum=0,m=1;
		//ÿ��������Ͳ�����maxsum�����������ʼ��һ��������
		for(int n:nums) {
				if(sum+n<=maxsum) {
						sum+=n;
				} else {
						sum=n;
						m+=1;
				}
		}
		return m;
}

public int splitArray(int[] nums, int m) {
		int l=0,r=0;
		//�Ͻ�Ϊ����ͣ��½�Ϊ�����е����ֵ
		for(int n:nums) {
				r+=n;
				if(l<n) {
						l=n;
				}
		}
		while(l<r) {
				int mid=l+(r-l)/2;
				if(splitNumber(nums,mid)<=m) {
						r=mid;
				} else {
						l=mid+1;
				}
		}
		return r;
}
```