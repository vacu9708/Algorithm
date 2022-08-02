# [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

## Recursively
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
