# [1. Two Sum](https://leetcode.com/problems/two-sum/)
~~~javascript
function twoSum(nums: number[], target: number): number[] {
    for(let i=0; i<nums.length; i++)
        for(let j=i+1; j<nums.length; j++) #nums[i] has already been used
            if(nums[i]+nums[j]==target)
                return [i, j]
};
~~~
