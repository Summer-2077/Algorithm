# decode_XORed_array

## 题目截图
 ![](decode_XORed_array.jpg)

## 思路 位运算

使用异或运算

异或运算性质：

1.相同数值异或，结果为`0`
2.任意数字与 `0` 进行异或， 结果为数值本身
3.异或本身满足交换律

由题目可知 `encoded[i] = arr[i] XOR arr[i + 1]`, 将等式两边同时异或 `arr[i]`，可得：
`encoded[i] XOR arr[i] = arr[i] XOR arr[i + 1] XOR arr[i]`
==>  **`encoded[i] XOR arr[i] = arr[i + 1]`**

所以知道了第一个` arr[0]` 及 `encoded` 数组，即可得到整个原数组



    
    class Solution:
        def decode(self, encoded: List[int], first: int) -> List[int]:
            res = [first]
            for num in encoded:
                first = num ^ first
                res.append(first)
            return res