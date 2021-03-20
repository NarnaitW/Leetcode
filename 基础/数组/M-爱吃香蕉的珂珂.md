# [爱吃香蕉的珂珂](https://leetcode-cn.com/problems/koko-eating-bananas/)

速度越小，时间越长，是单调升序列。  
找时间h对应的k的左边界。

```java
public int time(int[] piles, int k) {
	int t=0;
	for(int p:piles) {	//注意取上整的写法
		t += (p-1)/k+1;
	}
	return t;
}

public int minEatingSpeed(int[] piles, int h) {
    int l=1,r=1_000_000_000;
    while(l<r) {
    	int m=l+(r-l)/2;
    	if(time(piles,m)<=h) {
    		r=m;
    	} else {
    		l=m+1;
    	}
    }
    return r;
}
```
