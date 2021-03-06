# [寻找数组的中心索引](https://leetcode-cn.com/problems/find-pivot-index/)

思路：先计算整个数组的sum。  
然后从头开始，左侧和为0、右侧和为sum-nums[0]，遍历数组，左侧和依次加，右侧和依次减。  
相等时返回当前索引，若无相等返回-1

*更简单的判断条件：`leftsum == sum-leftsum-nums[i]`，即`2*leftsum+nums[i] == sum`，每次只改变leftsum*

## Python
```python
def pivotIndex(self, nums: List[int]) -> int:
        if nums is None:
            return -1
        leftsum,rightsum=0,sum(nums)-nums[0]
        i=0
        while(leftsum!=rightsum and i!=len(nums)-1):    # 循环终止条件：左侧和=右侧和 or 遍历完数组
            leftsum+=nums[i]                            # 注意：and和or不要搞错
            rightsum-=nums[i+1]
            i+=1;
        if leftsum==rightsum:
            return i
        else:
            return -1
```
## Java
```java
public int pivotIndex(int[] nums) {
    	if(nums==null) {
    		return -1;
    	}
    	int i,leftsum=0,rightsum=0;
        //求和用stream方法更简单
        //int total = Arrays.stream(nums).sum();
    	for(i=0;i<nums.length;i++) {
    		rightsum += nums[i];
    	}
    	rightsum-=nums[0];
    	for(i=0;i<nums.length-1;i++) {
    		if(leftsum==rightsum) {
    			return i;
    		}else {
    			leftsum+=nums[i];
    			rightsum-=nums[i+1];
    		}
    	}
    	if(leftsum==rightsum) {
    		return i;
    	}else {
    		return -1;
    	}
    }
```
[stream简介](https://www.jianshu.com/p/e429c517e9cb)
