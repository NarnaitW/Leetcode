# [寻找数组的中心索引](https://leetcode-cn.com/problems/find-pivot-index/)

思路：先计算整个数组的sum。  
然后从头开始，左侧和为0、右侧和为sum-nums[0]，遍历数组，左侧和依次加，右侧和依次减。  
相等时返回当前索引，若无相等返回-1

## Python
```python
def pivotIndex(self, nums: List[int]) -> int:
        if nums is None:
            return -1
        leftsum,rightsum=0,sum(nums)-nums[0]
        i=0
        while(leftsum!=rightsum and i!=len(nums)-1):
            leftsum+=nums[i]
            rightsum-=nums[i+1]
            i+=1;
        if leftsum==rightsum:
            return i
        else:
            return -1
```
