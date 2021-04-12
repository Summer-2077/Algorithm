
# longest_increasing_subsequence

## 题目截图
 ![](longest_increasing_subsequence.jpg)

## 思路一 动态规划

    class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        n, res = len(nums), 1
        dp = [1] * n
        for i in range(1, n):
            for j in range(i):
                if nums[i] > nums[j]:
                    dp[i] = max(dp[i], dp[j] + 1)
            res = max(res, dp[i])
        return res

