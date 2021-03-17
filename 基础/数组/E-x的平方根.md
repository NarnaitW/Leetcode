# [x的平方根](https://leetcode-cn.com/problems/sqrtx/)

方法一：  
用exp函数和log函数计算平方根，x<sup>1/2</sup>=e<sup>1/2*ln(x)</sup>  
*注意： 由于计算机无法存储浮点数的精确值（浮点数的存储方法可以参考 IEEE 754，这里不再赘述），而指数函数和对数函数的参数和返回值均为浮点数，因此运算过程中会存在误差。例如当x=2147395600时，e <sup>1/2*ln(x)</sup> 的计算结果与正确值46340相差 10<sup>-11</sup>，这样在对结果取整数部分时，会得到46339这个错误的结果。  
因此在得到结果的整数部分ans后，我们应当找出ans与ans + 1中哪一个是真正的答案。*  
时间复杂度*O(1)*，空间复杂度*O(1)*

```java
public int mySqrt(int x) {
    if (x == 0) {
        return 0;
    }
    int ans = (int) Math.exp(0.5 * Math.log(x));
    return (long) (ans + 1) * (ans + 1) <= x ? ans + 1 : ans;
}
```

方法二：  
用二分查找，设定上界为x，下界为0  
时间复杂度*O(logx)*，空间复杂度*O(1)*

```java
public int mySqrt(int x) {
    int l=0,r=x,ans=0;
    while(l<=r) {
        int m=(l+r)/2;
        if((long)m*m<=x) {  //必须有转换为长整型，否则m较大时计算不出来
            ans=m;
            l=m+1;
        } else {
            r=m-1;
        }
    }
    return ans;
}
```

方法三：
牛顿迭代法是一种快速求函数零点的方法，选取初始值x0，在(x0，f(x0))处作该点的切线，切线的零点作为下一次的选值，不断迭代，最终无限逼近函数零点。  
![avatar](https://assets.leetcode-cn.com/solution-static/69/69_fig1.png)
此题可看作求f=x<sup>2</sup>-C的非负零点，取x0=C，过(x0，x0<sup>2</sup>-C)作切线y=2x0(x-x0)+x0<sup>2</sup>-C=2*x0*x-(x0<sup>2</sup>+C)，下一次的取值即为切线零点1/2*(x0+C/x0)  
当两次取值相差很小的时候，迭代终止。

```java
public int mySqrt(int x) {
    if (x == 0) {
        return 0;
    }

    double C = x, x0 = x;
    while (true) {
        double xi = 0.5 * (x0 + C / x0);
        if (Math.abs(x0 - xi) < 1e-7) {
            break;
        }
        x0 = xi;
    }
    return (int) x0;
}
```
