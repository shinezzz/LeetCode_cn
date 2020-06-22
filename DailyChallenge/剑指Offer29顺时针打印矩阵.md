# DailyChallenge

## 剑指 Offer 29. 顺时针打印矩阵

`Easy`20200604

### Description

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

示例 1：

```python
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
```

示例 2：

```python
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
```

> 限制：
> 0 <= matrix.length <= 100
> 0 <= matrix[i].length <= 100

### Solution

参考官方解答

可以模拟打印矩阵的路径。初始位置是矩阵的左上角，初始方向是向右，当路径超出界限或者进入之前访问过的位置时，则顺时针旋转，进入下一个方向。

判断路径是否进入之前访问过的位置需要使用一个与输入矩阵大小相同的辅助矩阵 visited，其中的每个元素表示该位置是否被访问过。当一个元素被访问时，将 visited 中的对应位置的元素设为已访问。

如何判断路径是否结束？由于矩阵中的每个元素都被访问一次，因此路径的长度即为矩阵中的元素数量，当路径的长度达到矩阵中的元素数量时即为完整路径，将该路径返回。

```java
class Solution {
    public int[] spiralOrder(int[][] matrix) {
        if(matrix.length == 0){
            return new int[0];
        }

        int row = matrix.length;
        int col = matrix[0].length;
        int total = row * col;
        int[] res = new int[row * col];
        //模拟
        int[][] direction = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
        int direIndex = 0;
        int R = 0, C = 0;
        int nextR, nextC;
        boolean[][] visited = new boolean[row][col];
        for(int i = 0; i < total; i ++){
            res[i] = matrix[R][C];
            visited[R][C] = true;
            nextR = R + direction[direIndex][0];
            nextC = C + direction[direIndex][1];
            if(nextR >= row || nextR < 0 || nextC >= col || nextC < 0 || visited[nextR][nextC]){
                direIndex = (direIndex + 1) % 4;
            }
            R = R + direction[direIndex][0];
            C = C + direction[direIndex][1];
        }
        return res;

    }
}
```
