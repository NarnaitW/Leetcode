# [Ѱ���ظ���](https://leetcode-cn.com/problems/find-the-duplicate-number/)

��Ŀ�ٶ�������ֻ����һ���ظ��������������г����ظ���������������1��n��һ���֡��ظ�����СΪ1�����Ϊnums.length-1�����Կ��Զ�Ӧ�������±ꡣ  
�����±��0��n�����Կ������������飬���ǲ����±�i���Ԫ������cnt����i���ظ���Сʱ��cntһ��С�ڵ���i����i>=�ظ���ʱ��cntһ����i��  
���ԣ����ǿ��Ը���cnt���±�i�Ĵ�С��ϵ���ö��ֲ����ҵ��ظ�����  
ʱ�临�Ӷ�*O(nlogn)*���ռ临�Ӷ�*O(1)*

```java
public int findDuplicate(int[] nums) {
    int l=0,r=nums.length-1,ans=0;
    while(l<=r) {
    	int m=l+(r-l)/2;
    	int cnt=0;
    	for(int i=0;i<nums.length;i++) {
    		if(nums[i]<=m) {
    			cnt+=1;
    		}
    	}
    	if(cnt>m) {
    		r=m-1;
            ans=m;
    	} else {
    		l=m+1;
    	}
    }
    return ans;
}
```

��������[����ָ��](https://leetcode-cn.com/problems/find-the-duplicate-number/solution/kuai-man-zhi-zhen-de-jie-shi-cong-damien_undoxie-d/)  
�������Ŀ������������鵱��һ������������������±����ָ��Ԫ�ص�ָ�룬�������Ԫ��Ҳ����ָ�롣��**0**��ָ�룬ָ��**nums[0]**����**nums[0]**Ҳ��ָ�룬ָ��**nums[nums[0]]**��  
��Ϊ�ظ����Ĵ��ڣ�������һ���л���������ھ����ظ��������Կ����ÿ���ָ�롣  

```java
public int findDuplicate(int[] nums) {
		int slow=0,fast=0;
		do {
				slow=nums[slow];
				fast=nums[nums[fast]];
		} while(slow!=fast);
		slow=0;
		while(slow!=fast) {
				slow=nums[slow];
				fast=nums[fast];
		}
		return fast;
}
```