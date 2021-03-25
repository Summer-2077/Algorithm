# remove_nth_node_from_end_of_list

## 题目截图
 ![](remove_nth_node_from_end_of_list.jpg)

## 思路 自顶向下 分治 + 递归



    # Definition for singly-linked list.
    # class ListNode:
    #     def __init__(self, val=0, next=None):
    #         self.val = val
    #         self.next = next
    class Solution:
        def sortList(self, head: ListNode) -> ListNode:
            if not head or not head.next: return head
            mid = self.find_mid(head)
            left, right = head, mid.next
            mid.next = None
            left = self.sortList(left)
            right = self.sortList(right)
            return self.merge_two_list(left, right)
        
        def find_mid(self, head):
            # 找到中点，若为奇数返回中点，若为偶数，返回中心偏左节点
            if not head or not head.next: return head
            slow, fast = head, head.next.next
            while fast and fast.next:
                slow = slow.next
                fast = fast.next.next
            return slow
    
        def merge_two_list(self, l1, l2):
            dummy = head = ListNode(0)
            while l1 and l2:
                if l1.val < l2.val:
                    dummy.next = l1
                    dummy, l1 = dummy.next, l1.next
                else:
                    dummy.next = l2
                    dummy, l2 = dummy.next, l2.next
            if not l1: 
                dummy.next = l2
            if not l2:
                dummy.next = l1
            return head.next
            
