
# climbing_stairs

## 题目截图
 ![](climbing_stairs.jpg)

## 思路一 动态规划



    class Solution:
    def climbStairs(self, n: int) -> int:
        # 最后一步,到达第 n 个台阶，有两种可能 
        # 即：dp[n] = dp[n - 1] + dp[n - 2]
        # 初始值： dp[0] = 1, dp[1] = 1
        a, b = 1, 1  # 初始为 第 0 1 个台阶的值
        for i in range(1, n):
            a, b = b, a + b
        return b
