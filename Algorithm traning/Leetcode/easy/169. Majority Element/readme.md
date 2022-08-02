# [169. Majority Element](https://leetcode.com/problems/majority-element/)

## Very slow
Because linked lists are used instead of arrays in python
~~~python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        hashmap=[0 for i in range(5*10**4)]
        for num in nums:
            hashmap[num]+=1
        
        for num, count in enumerate(hashmap):
            if hashmap[num]>len(nums)//2:
                return num
~~~

## First solution
~~~python
class Solution:
    def majorityElement(self, nums):
        hashmap={}
        # Count appearances of numbers
        for num in nums:
            hashmap[num]=hashmap.get(num, 0) + 1
        
        # Find the majority element
        for key in hashmap.keys():
            if hashmap[key] > len(nums)//2:
                return key
~~~
