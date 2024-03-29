# [用Rand7()实现Rand10()](https://leetcode-cn.com/problems/implement-rand10-using-rand7/)

## 随机数产生原理
计算机程序中的随机数通常是伪随机数，常用的方法是线性同余法，即 y=(ax+b)%m+n ，a是一个较大的素数，x是种子，无输入时常用时钟  
本题可以用以上思路

## 思路
需要产生1-10的随机数，可以让m=10，n=1  
我们可以调用两次Rand7()，让它们相乘，可以得到 [1,49] 范围的整数  
因为49不是10的整数倍，所以得到的随机数概率是不同的，因此需要去掉 [41,49] 中的整数，只保留 [1,40] 的整数

## Java
```java
public int rand10() {
    int num;
    do {
        num=(rand7()-1)*7+rand7(); //相乘的话，调用次数较多时会出错；换成两个随机数相加，范围仍然是[1,49]
    } while(num>40);
    return num%10+1;
}
```

## 方法二
第一次产生 [1,49] 范围的整数时，需要舍弃41~49，即1~9，一共9个整数，舍弃的概率为9/49=0.184  
如果在1~9的基础上，再产生一次随机数，范围是 [1,63] ,这时需要舍弃 [61,63] 3个整数，舍弃的概率为3/63=0.04，比第一次舍弃的概率要小  
舍弃的概率也就是需要再次循环的概率，概率越小，调用次数较多时，所需要的平均时间就越少  
所以，可以在方法一的基础上，当得到 [41,49] 时，再产生一次随机数，对算法进行优化
