
# longest_palindromic_substring

## 题目截图
 ![](longest_palindromic_substring.jpg)

## 思路一 动态规划
此题需要快速的判断子串是否是回文
- 状态转移方程： dp[i][j] = s[i] == s[j] and dp[i + 1][j - 1]
- 边界条件，当 j - i < 1 时，即闭区间长度为 1 或者为空，此子串是回文
- 遍历顺序，应当是从左至右逐列

遇到此类题最好先画个动态规划的表格，确定填表顺序

![](https://pic.leetcode-cn.com/7e9d1f1dbe2095b0609233faa03b224ab32adf832515de1ce15b496f2cbdf0ab-image.png)

    class Solution:
    def longestPalindrome(self, s: str) -> str:
        # 动态规划
        # 此题需要快速的判断子串是否是回文
        # 状态转移方程： dp[i][j] = s[i] == s[j] and dp[i + 1][j - 1]
        # 边界条件，当 j - i < 1 时，即闭区间长度为 1 或者为空，此子串是回文
        # 遇到
        length = len(s)
        if length < 2:
            return s
        max_length = 1
        start_index = 0
        dp = [[False for _ in range(length)] for _ in range(length)]
        for j in range(length):
            dp[j][j] = True
            for i in range(j):
                if s[i] == s[j]:
                    if j - i < 3:
                        dp[i][j] = True
                    elif dp[i + 1][j - 1]:
                        dp[i][j] = True
                if dp[i][j]:
                    if j - i + 1 > max_length:
                        max_length = j - i + 1
                        start_index = i
        return s[start_index:start_index + max_length]

