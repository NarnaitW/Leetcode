# [�����㽶������](https://leetcode-cn.com/problems/koko-eating-bananas/)

�ٶ�ԽС��ʱ��Խ�����ǵ��������С�  
��ʱ��h��Ӧ��k����߽硣

```java
public int time(int[] piles, int k) {
		int t=0;
		for(int p:piles) {			//ע��ȡ������д��
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