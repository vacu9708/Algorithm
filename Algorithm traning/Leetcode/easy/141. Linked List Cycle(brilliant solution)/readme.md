### [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

## First solution(slower)
Using a dictionary that has information on if a node has previously been visited or not
~~~python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        pointer=head
        visiteds={}
            
        pointer=head
        while True:
            visiteds[id(pointer)]=True
            pointer=pointer.next
            if not pointer:
                return False
            try:
                if visiteds[id(pointer)]:
                    return True
            except:
                visiteds[id(pointer)]=False
~~~

## Brilliant solution
Using a slow pointer and a fast pointer
~~~python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow_pointer=fast_pointer=head
        while fast_pointer and fast_pointer.next:
            fast_pointer=fast_pointer.next.next
            slow_pointer=slow_pointer.next
            if fast_pointer==slow_pointer:
                return True
        return False
~~~
