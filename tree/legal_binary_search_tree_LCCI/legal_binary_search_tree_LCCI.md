# legal_binary_search_tree_LCCI

## 题目截图
 ![](legal_binary_search_tree_LCCI.jpg)

## 思路 二叉树中序遍历



    # Definition for a binary tree node.
    # class TreeNode:
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None
    
    class Solution:
        def isValidBST(self, root: TreeNode) -> bool:
            # 中序遍历
            stack, prev = [], float("-INF")
            while stack or root:
                # 将左侧节点都入栈
                while root:
                    stack.append(root)
                    root = root.left
                root = stack.pop()
                if prev >= root.val:
                    return False
                prev = root.val
                # 此处不用判断右子节点是否存在，因为不存在的话刚好需要将 root 变为 0
                root = root.right
            return True

## 思路 递归



    # Definition for a binary tree node.
    # class TreeNode:
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None
    
    class Solution:
        def isValidBST(self, root: TreeNode) -> bool:
            def dfs(root, low, upper):
                if not root: return True
                if root.val <= low or root.val >= upper:
                    return False
                if not dfs(root.left, low, root.val):
                    return False
                if not dfs(root.right, root.val, upper):
                    return False
                return True
            return dfs(root, float("-inf"), float("inf"))
