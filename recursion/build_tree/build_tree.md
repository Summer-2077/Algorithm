# build_tree

## 题目截图
 ![](build_tree.jpg)

## 思路 递归

- 时间复杂度：`O(N)`,对`N`个节点进行了遍历
- 空间复杂度：`O(N)`,栈最大深度为`N`
  
  
    # Definition for a binary tree node.
    # class TreeNode:
    #     def __init__(self, val=0, left=None, right=None):
    #         self.val = val
    #         self.left = left
    #         self.right = right
    class Solution:
        def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
            # 递归，递归参数为前序中序的索引,采用闭区间
            dic = {}
            for i, x in enumerate(inorder):
                dic[x] = i
            def dfs(pre_l, pre_r, in_l, in_r):
                # 若前序为空，则返回
                if pre_l > pre_r:
                    return None
                # 根节点
                node = TreeNode(preorder[pre_l])
                node.left = dfs(pre_l + 1, pre_l + dic[preorder[pre_l]] - in_l, in_l, dic[preorder[pre_l]] - 1)
                node.right = dfs(pre_l + dic[preorder[pre_l]] - in_l + 1, pre_r, dic[preorder[pre_l]] + 1, in_r)
                return node
            return dfs(0, len(preorder) - 1, 0, len(inorder) - 1)
