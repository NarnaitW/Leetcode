# [寻找重复数](https://leetcode-cn.com/problems/find-the-duplicate-number/)

题目假定数组中只包含一个重复的数，即数组中除了重复数，其余数就是1到n的一部分。重复数最小为1，最大为nums.length-1，所以可以对应到数组下标。  
数组下标从0到n，可以看作是升序数组，考虑不比下标i大的元素数量cnt，当i比重复数小时，cnt一定小于等于i；当i>=重复数时，cnt一定比i大。  
所以，我们可以根据cnt与下标i的大小关系，用二分查找找到重复数。  
时间复杂度*O(nlogn)*，空间复杂度*O(1)*

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

方法二：[快慢指针](https://leetcode-cn.com/problems/find-the-duplicate-number/solution/kuai-man-zhi-zhen-de-jie-shi-cong-damien_undoxie-d/)  
将这个题目给的特殊的数组当作一个链表来看，数组的下标就是指向元素的指针，把数组的元素也看作指针。如**0**是指针，指向**nums[0]**，而**nums[0]**也是指针，指向**nums[nums[0]]**。  
因为重复数的存在，该链表一定有环，环的入口就是重复数。所以可以用快慢指针。  

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