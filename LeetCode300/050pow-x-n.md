# 50. Pow(x, n)）

https://leetcode-cn.com/problems/powx-n/description/

## 题目描述

实现 pow(x, n) ，即计算 x 的 n 次幂函数。

```r
示例 1:

输入: 2.00000, 10
输出: 1024.00000
示例 2:

输入: 2.10000, 3
输出: 9.26100
示例 3:

输入: 2.00000, -2
输出: 0.25000
解释: 2-2 = 1/22 = 1/4 = 0.25
说明:

-100.0 < x < 100.0
n 是 32 位有符号整数，其数值范围是 [−231, 231 − 1] 。
```

## 前置知识

- 递归
- 位运算

## 公司

- 阿里
- 腾讯
- 百度
- 字节

## 代码

快速幂

```java
class Solution {
    public double myPow(double x, int n) {
        boolean flag = n < 0;
        long N = Math.abs((long)n);
        double res = 1.0;
        while(N > 0) {
            if((N & 1) == 1) {
                res = res * x;
            }
            x = x * x;
            N = N >> 1;
        }
        if(flag) return 1 / res;
        return res;

    }
}
```