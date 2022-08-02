# [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)

## Using hashmap (first solution)
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

## More effective
~~~python
class Solution:
    def getIntersectionNode(self, headA, headB):
        pA = headA # 2 pointers
        pB = headB

        '''The 2 pointers will meet on the second traversal eventually.
        either on the intersect or null pointer'''
        while pA != pB:
            # if either pointer hits the end, switch head
            # if not hit the end, just move on to next
            pA = headB if pA == None else pA.next  
            pB = headA if pB == None else pB.next

        return pA
~~~
