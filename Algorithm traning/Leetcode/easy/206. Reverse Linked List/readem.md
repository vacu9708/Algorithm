# [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

## Recursively (first solution)
~~~python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        def DFS(prev_node, current_node):
            if not current_node:
                return prev_node # new head
            
            new_head=DFS(current_node, current_node.next)
            current_node.next=prev_node
            return new_head

        return DFS(None, head) # Return new head
~~~

## Iteratively (more effective)
~~~python
class Solution:
    def reverseList(self, head):
        prev = None
        while head:
            next_node=head.next #Store the next node before changing head.next
            head.next=prev
            prev=head
            head=next_node
        return prev
~~~
