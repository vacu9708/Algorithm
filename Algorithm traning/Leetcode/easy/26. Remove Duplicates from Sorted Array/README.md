# [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
~~~Python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        i_to_put=0 # index to put
        n_to_put=nums[0] # number to put
        for i in range(len(nums)):
            if nums[i]!=n_to_put:
                nums[i_to_put]=n_to_put
                i_to_put+=1
                n_to_put=nums[i]
        nums[i_to_put]=nums[-1] # last index
        return i_to_put+1
~~~
