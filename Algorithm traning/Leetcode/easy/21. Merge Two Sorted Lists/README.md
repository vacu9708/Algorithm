# [21. Merge Two sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

## This solution is similar to how the merge sort works
~~~Python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def mergeTwoLists1(self, list1, list2):
    head = cur = ListNode()
    while list1 and list2:
        if list1.val < list2.val:
            cur.next = list1
            list1 = list1.next
        else:
            cur.next = list2
            list2 = list2.next
        cur = cur.next
    cur.next = list1 if list1 else list2 # remaining elements
    return head.next
~~~

~~~Python
# recursively    
def mergeTwoLists2(self, list1, list2):
    if not list1 or not list2:
        return list1 or list2
    if list1.val < list2.val:
        list1.next = self.mergeTwoLists(list1.next, list2)
        return list1
    else:
        list2.next = self.mergeTwoLists(list1, list2.next)
        return list2
~~~
