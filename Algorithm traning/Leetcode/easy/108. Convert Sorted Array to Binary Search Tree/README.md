# [108. Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)

## Iteratively
~~~javascript
var sortedArrayToBST = function(nums) {
    let mid=Math.floor(nums.length/2)
    let root=new TreeNode(nums[mid])
    let current=root
    for(let i=mid-1; i>=0; i--){
        current.left=new TreeNode(nums[i])
        current=current.left
    }
    current=root
    for(let i=mid+1; i<nums.length; i++){
        current.right=new TreeNode(nums[i])
        current=current.right
    }
    return root
};
~~~

## Recursively
~~~javascript
if (!nums.length)
        return null
    
    let mid=Math.floor(nums.length/2)
    let node=new TreeNode(nums[mid])
    node.left=sortedArrayToBST(nums.slice(0,mid))
    node.right=sortedArrayToBST(nums.slice(mid+1,nums.length))
    return node
~~~
