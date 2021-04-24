# implement_strStr()

## 题目截图
 ![](implement_strStr().jpg)

## 思路 KMP算法

举例：

原串 `string`: `a a b a a b a a f`

匹配串 `pattern`: `a a b a a f`

匹配串 `next` 数组： `0 1 0 1 2 0`

`next` 数组的意义是以该位置字符结尾的最长相等前后缀(字符串本身不是自己的前后缀)，且如例子中当`b` 与 `f` 不匹配时，应当跳到前一个字符结尾的子串的最长匹配前缀的后一个字符进行匹配(即next(j - 1) :`b`的位置)。
而该字符的索引即为不匹配字符前一个字符的`next`数值。

构建 `next` 数组：

构建 `next` 数组的过程本身也是字符匹配的过程。

使用两个变量 `i` , `j` ; `j` 代表 **前缀末尾**， `i` 代表**后缀末尾**,

当出现后缀末尾与前缀末尾不匹配时，参考 kmp 匹配的过程，此时后缀字符串相当于 string, 前缀字符串相当于 pattern，所以应当把 j 退回到 next(j - 1)位置继续进行匹配，直到匹配成功或退回第一个位置





    class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if not needle: return 0
        length_s, length_p = len(haystack), len(needle)
        next_list = [0] * length_p
        j = 0
        # 生成 next 数组
        for i in range(1, length_p):
            # 当 i , j 不匹配
            # 往前回溯直到到了第一个位置或者字符匹配
            while j > 0 and needle[i] != needle[j]:
                # 回退到 i 之前部分已匹配字符串的最长前缀后一个位置
                j = next_list[j - 1]
            # 继续进行匹配，最差情况为回退到第一个位置进行匹配
            if needle[i] == needle[j]:
                j += 1
            # 不管字符匹配还是到第一个位置，此时 i 位置上的值应当为最长匹配长度 0 或者 j(j 已经进行了j + 1)
            next_list[i] = j
        # 进行匹配
        j = 0
        for i in range(length_s):
            while j > 0 and needle[j] != haystack[i]:
                j = next_list[j - 1]
            if needle[j] == haystack[i]:
                j += 1
            if j == length_p:
                return i - length_p + 1
        return -1



