# maximum_depth_of_binary_tree

## 题目截图
 ![](maximum_depth_of_binary_tree.jpg)

## 思路一 递归


    # Definition for a binary tree node.
    # class TreeNode:
    #     def __init__(self, val=0, left=None, right=None):
    #         self.val = val
    #         self.left = left
    #         self.right = right
    class Solution:
        def maxDepth(self, root: TreeNode) -> int:
            if not root:
                return 0
            return max(self.maxDepth(root.left), self.maxDepth(root.right)) + 1
            

## 思路二 BFS


    # Definition for a binary tree node.
    # class TreeNode:
    #     def __init__(self, val=0, left=None, right=None):
    #         self.val = val
    #         self.left = left
    #         self.right = right
    class Solution:
        def maxDepth(self, root: TreeNode) -> int:
            if not root:
                return 0
            depth, queue = 0, [root]
            while queue:
                depth += 1
                length = len(queue)
                for i in range(length):
                    node = queue.pop(0)
                    if node.left:
                        queue.append(node.left)
                    if node.right:
                        queue.append(node.right)
            return depth
            
            
