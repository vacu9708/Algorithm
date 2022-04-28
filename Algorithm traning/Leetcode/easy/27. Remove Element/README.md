# [27. Remove Element](https://leetcode.com/problems/remove-element/submissions/)
## My first solution
~~~Python
class Solution:
    def removeElement(self, nums, val: int) -> int:
        removed_elements=0
        i=0
        length=len(nums)
        while i<length:
            if nums[i]==val:
                how_many_to_move=0
                j=i
                while j<length and not nums[j]!=val:
                    how_many_to_move+=1
                    removed_elements+=1
                    j+=1
                for j in range(j, length):
                    nums[j-how_many_to_move]=nums[j]
                length-=how_many_to_move
            else:
                i+=1
        return len(nums)-removed_elements
~~~
## Better solution
~~~python
def removeElement(self, nums, val):
    i_to_put = 0
    for x in nums:
        if x != val:
            nums[i] = x
            i_to_put += 1
    return i_to_put
~~~
