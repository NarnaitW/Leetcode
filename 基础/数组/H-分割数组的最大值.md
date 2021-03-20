# [分割数组的最大值](https://leetcode-cn.com/problems/split-array-largest-sum/)

使用二分查找的思路：  
要找到m个子数组和的最大值，它的上界就是整个数组的和，下界是数组中元素的最大值。  
我们可以考虑，给定子数组和的最大值，看看能把数组分为几个非空连续子数组。  
如果分割的子数组数目>m，说明给定的最大值太小；反之，如果子数组数目<=m，则要找的目标值应该更小。  
时间复杂度*O(nlog(sum-maxn))*，空间复杂度*O(1)*

```java
public int splitNumber(int[] nums, int maxsum) {
	int sum=0,m=1;
	//每个子数组和不大于maxsum，如果大于则开始下一个子数组
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
	//上界为数组和，下界为数组中的最大值
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

[在 D 天内送达包裹的能力](https://leetcode-cn.com/problems/capacity-to-ship-packages-within-d-days/)  
解题方法与上相同

[制作 m 束花所需的最少天数](https://leetcode-cn.com/problems/minimum-number-of-days-to-make-m-bouquets/)  
思路相同，给定时间计算能做几束花  
```java
    public int bunchNumber(int[] bloomDay, int k, int day) {
        int bcnum=0, fn=0;
        for(int b:bloomDay) {
            if(b<=day) {
                fn += 1;
            } else {
                bcnum+=fn/k;
                fn=0;
            }
        }
        bcnum+=fn/k;
        return bcnum;
    }
    public int minDays(int[] bloomDay, int m, int k) {
        if(m*k>bloomDay.length) {
            return -1;
        }
        int l=0,r=0;
        for(int b:bloomDay) {
            r = b>r ? b:r;
        }
        while(l<r) {
            int mid=l+(r-l)/2;
            if(bunchNumber(bloomDay,k,mid)>=m) {
                r=mid;
            } else {
                l=mid+1;
            }
        }
        return r;
    }
```
