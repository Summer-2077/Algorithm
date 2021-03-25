# palindrome_linked_list

## 题目截图
 ![](palindrome_linked_list.jpg)

## 思路 找中点 + 翻转 + 遍历比较



    # Definition for singly-linked list.
    # class ListNode:
    #     def __init__(self, val=0, next=None):
    #         self.val = val
    #         self.next = next
    class Solution:
        def isPalindrome(self, head: ListNode) -> bool:
            # 首先找到链表中点，再逐个比较
            if not head.next: return True
            low, fast = head, head.next.next
            while fast and fast.next:
                low = low.next
                fast = fast.next.next
            head2 = low.next
            low.next = None
    
            # 将链表一反转
            head1 = head2
            while head2.next:
                tmp = head2.next.next
                head2.next.next = head1
                head1 = head2.next
                head2.next = tmp
            
            # 遍历比较两链表
            while head1 and head:
                if head1.val != head.val:
                    return False
                head1 = head1.next
                head = head.next
    
            return True
        
            
## 思路二 递归


    # Definition for singly-linked list.
    # class ListNode:
    #     def __init__(self, val=0, next=None):
    #         self.val = val
    #         self.next = next
    class Solution:
        def isPalindrome(self, head: ListNode) -> bool:
            self.front_pointer = head
            def recursively_check(node):
                if node:
                    if not recursively_check(node.next):
                        return False
                    if self.front_pointer.val != node.val:
                        return False
                    self.front_pointer = self.front_pointer.next
                return True
            return recursively_check(head)