# [旋转矩阵](https://leetcode-cn.com/problems/rotate-matrix-lcci/)

向右旋转90度，矩阵中任意一个元素[i，j]经过4次旋转会回到原来位置，所以只需要考虑交换这4个位置的元素  
位置[i，j]的元素，经旋转后，到达位置[j，n-1-i]，同理，可推出，  
位置[j，n-1-i]，会到达位置[n-1-i，n-1-j]  
位置[n-1-i，n-1-j]，会到达位置[n-1-j，i]
位置[n-1-j，i]，会到达位置[i，j]  
所以，在循环中对这4个位置的元素交换即可实现旋转90度。  
因为一次交换4个元素，所以只需要对矩阵左上角的1/4循环即可，若n为奇数，则只需要行取下整，列取上整即可

## Java
```java
public void rotate(int[][] matrix) {
    int n=matrix.length;
    for(int i=0;i<n/2;i++)        //java里n/2取下整，即若n=3，n/2=1，i只能取0
      for(int j=0;j<(n+1)/2;j++) {
        int temp=matrix[i][j];
        matrix[i][j]=matrix[n-1-j][i];
        matrix[n-1-j][i]=matrix[n-1-i][n-1-j];
        matrix[n-1-i][n-1-j]=matrix[j][n-1-i];
        matrix[j][n-1-i]=temp;
      }
}
```

## Python
```python
def rotate(self, matrix: List[List[int]]) -> None:
    """
    Do not return anything, modify matrix in-place instead.
    """
    n=len(matrix)
    for i in range(0,int(n/2)):           # (0,1)则i可取0，1；range(0,1)则i只能取0
      for j in range(0,int((n+1)/2)):     # range里必须是整数
        temp=matrix[i][j];
        matrix[i][j]=matrix[n-1-j][i];
        matrix[n-1-j][i]=matrix[n-1-i][n-1-j];
        matrix[n-1-i][n-1-j]=matrix[j][n-1-i];
        matrix[j][n-1-i]=temp;
```
