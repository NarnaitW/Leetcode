# [合并区间](https://leetcode-cn.com/problems/merge-intervals/)  
需要对区间按左端点的顺序排序

## Python  
```python
def merge(self, intervals: List[List[int]]) -> List[List[int]]:
    if intervals==[] or len(intervals)==1:
        return intervals
    intervals.sort(key=lambda interval: interval[0])    # list内置sort方法，以区间左端点排序，时间复杂度O(nlogn)
    res=[]
    for interval in intervals:
        # 如果res为空，或该区间与上一区间不重合，即该区间左端点>上一区间右端点，则直接添加
        if not res or interval[0]>res[-1][1]:
            res.append(interval)
        else:
            res[-1][1]=max(interval[1],res[-1][1])
    return res
```

## Java
```java
```
