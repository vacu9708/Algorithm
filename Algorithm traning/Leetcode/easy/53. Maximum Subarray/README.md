# [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
~~~javascript
var maxSubArray = function(nums) {
    len_nums=nums.length;
    for(i=1; i<len_nums; i++){
            if(nums[i-1] > 0)
                nums[i] += nums[i-1]
    }
    max=0;
    for(i=1; i<len_nums; i++)
        if(nums[i]>nums[max])
            max=i;
    return nums[max]
};
~~~

## Time limit(brute force)
~~~javascript
var maxSubArray = function(nums) {
    max=(10**4)*-1;
    temp_max=0;
    len_nums=nums.length;
    for(i=0; i<len_nums; i++)
        for(j=i; j<len_nums; j++){
            for(k=i; k<=j; k++)
                temp_max+=nums[k]
            if(temp_max>max)
                max=temp_max;
            temp_max=0;
        }
    return max
};
~~~

## If a subarray can be discreet not only contiguous
~~~javascript
var maxSubArray = function(nums) {
  nums.sort((a,b)=>{
      if(a<b)
          return 1;
      else
          return -1;
  })
  len_nums=nums.length;
  max=nums[0]
  console.log(nums);
  for(i=1; i<len_nums; i++)
      if(max+nums[i]<=max)
          return max;
      else{
          console.log('index '+i);
          max+=nums[i];
      }
};

console.log(maxSubArray([-2, 1, -3, 4, -1, 2, 1, -5, 4]));
~~~

## If a subarray can be discreet not only contiguous(brute force)
~~~javascript
let max = 0;
let answer = new Array(9);
let truth_table = new Array(9);
let dfs = function (level, temp_max, nums) {
  if (level == nums.length) { // Backtracking
    if (temp_max > max) {
      max = temp_max;
      for (let i = 0; i < 9; i++)
        answer[i] = truth_table[i];
      //console.log(answer+' '+max);
    }
    return;
  }

  for (let i = 0; i <= 1; i++) {
    truth_table[level] = i;
    if (i){
      dfs(level + 1, temp_max + nums[level], nums)
    else
      dfs(level + 1, temp_max, nums)
  }
}

var maxSubArray = function (nums) {
  dfs(0, 0, nums);
  console.log(answer+' '+max);
};

maxSubArray([-2, 1, -3, 4, -1, 2, 1, -5, 4]);
~~~
