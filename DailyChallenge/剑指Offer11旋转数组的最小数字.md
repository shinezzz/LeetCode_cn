# DailyChallenge

## 剑指 Offer 11. 旋转数组的最小数字

`Easy`20200722

### Description

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。  

```matlab
示例 1：

输入：[3,4,5,1,2]
输出：1
示例 2：

输入：[2,2,2,0,1]
输出：0
```

**链接**：<https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof>

### Solution

二分查找。注意从右边开始缩进。因为如果数组没有旋转，从左边开始缩进，就会错过最小值。

还是套用二分模板，具体见GitHub地址:<https://github.com/shinezzz/LeetCode-Topic>

```java
while(low <= high){
    int mid = low + (high - low) / 2;
    if(numbers[mid] < target) ...;
    else if(numbers[mid] > target ) ...;
    else if(numbers[mid] == target) ...;
}
```

**解题代码**：

```java
class Solution {
    public int minArray(int[] numbers) {
        int n = numbers.length;
        int low = 0, high = n - 1;
        while(low <= high){
            int mid = low + (high - low) / 2;
            int target = numbers[high];
            // System.out.println("target:"+ target);
            // System.out.println("mid:"+ numbers[mid]);

            if(numbers[mid] < target) {
                if(mid == 0 || numbers[mid - 1] >= target) return numbers[mid];
                else high = mid - 1;
            }
            else if(numbers[mid] > target ) low = mid + 1;
            else if(numbers[mid] == target) high--;
        }
        return numbers[low];
    }
}
```
