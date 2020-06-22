# DailyChallenge

## 剑指 Offer 46. 把数字翻译成字符串

`Medium`20200609

### Description

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

示例 1:

```matlab
输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
```

> 提示：
>
> 0 <= num < 231

### Solution

1. 动态规划 + 数组
    dp[i] 表示从第0位到第i位可以有多少中字母。
    考虑第i位
   - 可以单独作为一位来翻译
   - 如果第 i - 1 位和第 i 位组成的数字在 10 到 25 之间，可以把这两位连起来翻译
   - dp[i] = dp[i - 1] + dp[i - 1](符合条件2的情况下)

    ```java
    class Solution {
        public int translateNum(int num) {
            // dp[i]前i个字母能翻译几种
            int[] numArray = new int[32];
            int id = 31;
            while(num > 0){
                numArray[id--] = num%10;
                num = num / 10;
            }
            // dp数组的长度我多设置了1，表示一下前0个字母，这样思考好思考一点
            int[] dp = new int[32 - id];
            int len = dp.length;
            if(len == 1) return 1;
            Arrays.fill(dp, 0);
            dp[0] = 1;
            dp[1] = 1;
            for(int i = 2; i < len ; i++){
                dp[i] += dp[i - 1];
                if(isLetter(numArray[id + i - 1], numArray[id + i])){
                    dp[i] += dp[i - 2];
                }
            }
            return dp[len - 1];
        }
        public boolean isLetter(int a, int b){
            if(a == 1 ||(a == 2 && b < 6)){
                return true;
            }
            return false;
        }
    }
    ```

2. 动态规划 + 字符串 + 滚动数组
   官方题解和第一种方法两种不同
   - 用字符串存储num的每一位
   - 用了滚动数组替代dp，减小空间复杂度

    ```java
    class Solution {
        public int translateNum(int num) {
            String src = String.valueOf(num);
            int p = 0, q = 0, r = 1;
            for (int i = 0; i < src.length(); ++i) {
                p = q;
                q = r;
                r = 0;
                r += q;
                if (i == 0) {
                    continue;
                }
                String pre = src.substring(i - 1, i + 1);
                if (pre.compareTo("25") <= 0 && pre.compareTo("10") >= 0) {
                    r += p;
                }
            }
            return r;
        }
    }
    ```

3. 递归
    递归，根据末尾两位来分。

    ```java
    class Solution {
        public int translateNum(int num) {
            if(num <= 9){
                return 1;
            }
            //根据末尾两位分
            int theLastTwo = num % 100;
            if(theLastTwo >= 26 || theLastTwo <= 9){
                return translateNum(num / 10);
            }else{
                return translateNum(num / 10) + translateNum(num / 100);
            }
        }
    }
    ```
