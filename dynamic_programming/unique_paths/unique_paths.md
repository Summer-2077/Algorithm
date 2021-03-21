# unique_paths

## 题目截图
 ![](unique_paths.jpg)

## 思路 动态规划
- 状态 `dp[i][j]`  代表以到达该位置的路径数
- 状态转移方程：`dp[i][j] = dp[i - 1][j] + dp[i][j - 1]`
- 边界条件：`i == 0 or j == 0 : dp[i][j] = 1`


    class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        # 经典动态规划
        # 最后一步只能是该坐标的左边或上边到达
        # dp[i][j] 表示到达 [i][j] 的路径数
        # 状态转移方程： dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        # 边界条件： i == 0 or j == 0 : dp[i][j] = 1
        dp = [[1 for _ in range(n)] for _ in range(m)]
        # 遍历顺序，从左到右，从上到下
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        return dp[-1][-1]

