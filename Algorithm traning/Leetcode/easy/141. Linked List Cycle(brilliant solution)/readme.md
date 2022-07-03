### [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

## Solution 1
Using a dictionary that has information on if a node has previously been visited or not
~~~python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        pointer=head
        visiteds={}
        while pointer:
            visiteds[pointer]=True
            pointer=pointer.next
            try:
                if visiteds[pointer]:
                    return True
            except:
                visiteds[pointer]=False
        return False
~~~

## Solution 2
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
