# [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)

## Using hashmap
~~~python
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        hashmap={}
        # Store the addresses of list A
        while True:
            if not headA:
                break
            
            hashmap[headA]=True
            headA=headA.next
        
        # Find if list B has an element on the same address as an element of list A
        while True:
            if not headB:
                return headB
            
            if headB in hashmap:
                return headB
            else:
                headB=headB.next
~~~
