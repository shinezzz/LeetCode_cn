# DailyChallenge

## 剑指 Offer 64 求1+2+…+n  

`Medium`20200602

### Description

求 `1+2+...+n` ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

**示例 1：**

```python
输入: n = 3
输出: 6
```

### Solution

短路效应：**条件与 && 具有短路原则**，即在第一个条件语句为 false 的情况下不会去执行第二个条件语句。

```java
class Solution {
    public int sumNums(int n) {
        boolean x = n > 1 && (n += sumNums(n-1)) > 0;
        return n;
    }
}
```
