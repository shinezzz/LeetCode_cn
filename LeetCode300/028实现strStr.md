# 28. 实现 strStr()

## 题目描述

实现 strStr() 函数。

给你两个字符串 haystack 和 needle ，请你在 haystack 字符串中找出 needle 字符串出现的第一个位置（下标从 0 开始）。如果不存在，则返回  -1 。

 

说明：

> 当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。
> 对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与 C 语言的 strstr() 以及 Java 的 indexOf() 定义相符。

 
```r
示例 1：

输入：haystack = "hello", needle = "ll"
输出：2

示例 2：

输入：haystack = "aaaaa", needle = "bba"
输出：-1

示例 3：

输入：haystack = "", needle = ""
输出：0
```
 

提示：

- 0 <= haystack.length, needle.length <= 5 * 10^4
- haystack 和 needle 仅由小写英文字符组成

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/implement-strstr
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 代码

### 1. 暴力，两重循环

```java
class Solution {
    public int strStr(String haystack, String needle) {
        int n1 = haystack.length();
        int n2 = needle.length();
        if(n2 == 0) return 0;
        if(n1 < n2) return -1;
        for(int i = 0; i <= n1 - n2; i++) {
            for(int j = 0; j < n2; j++) {
                if(haystack.charAt(i + j) != needle.charAt(j)) break;
                if(haystack.charAt(i + j) == needle.charAt(j)) {
                    if(j == n2 - 1) return i;
                }
            }
        }
        return -1;
    }
}
```

### 2. KMP 算法

```java
class Solution {
    public int strStr(String s, String p) {
        int n1 = s.length();
        int n2 = p.length();
        if(n2 == 0) return 0;
        if(n1 < n2) return -1;
        int[] ne = new int[n2 + 10];

        // 预处理过程
        Arrays.fill(ne, -1);
        for(int i = 1, j = -1; i < n2; i++) {
            while(j > -1 && p.charAt(i) != p.charAt(j + 1)) j = ne[j];
            if(p.charAt(i) == p.charAt(j + 1)) j++;
            ne[i] = j;
        }

        // 匹配过程
        for(int i = 0, j = -1; i < n1; i++) {
            while(j > -1 && s.charAt(i) != p.charAt(j + 1)) j = ne[j];
            if(s.charAt(i) == p.charAt(j + 1)) j++;
            if(j == n2 - 1) {
                return i - n2 + 1;
            }
        }
        return -1;
    }
}
```

### 3. 字符串哈希

```java
class Solution {
    public int strStr(String s, String p) {
        int n1 = s.length();
        int n2 = p.length();
        if(n2 == 0) return 0;
        if(n1 < n2) return -1;
        int T = 131;
        int[] h = new int[n1 + 10];
        int[] q = new int[n2 + 10];
        int[] t = new int[100010];
        t[0] = 1;
        for(int i = 1; i <= Math.max(n1, n2); i++) {
            if(i <= n1) h[i] = h[i - 1] * T + s.charAt(i - 1);
            if(i <= n2) q[i] = q[i - 1] * T + p.charAt(i - 1);
            t[i] = t[i - 1] * T;
        }

        for(int i = 1; i + n2 - 1 <= n1; i++) {
            if(h[i + n2 - 1] - h[i - 1] * t[n2] == q[n2]) return i - 1;
        }
        return -1;
    }
}
```