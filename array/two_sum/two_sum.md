# Two_Sum

## 题目截图
 [](/two_sum.jpg)

## 思路一 字典


    class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        dic = {}
        for i, num in enumerate(nums):
            if (target - num) in dic:
                return[dic[target - num], i]
            dic[num] = i
        return []
