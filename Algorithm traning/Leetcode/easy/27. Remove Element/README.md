[27. Remove Element](https://leetcode.com/problems/remove-element/submissions/)
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
                for k in range(j, length):
                    nums[k-how_many_to_move]=nums[k]
                length-=how_many_to_move
            else:
                i+=1
        return len(nums)-removed_elements
~~~
