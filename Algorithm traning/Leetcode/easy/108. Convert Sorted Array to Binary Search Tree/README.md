# [108. Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)

## Divide and conquer
~~~javascript
/*
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
*/

var sortedArrayToBST = function(nums) {
    if (!nums.length)
            return null

        let mid=Math.floor(nums.length/2)
        let node=new TreeNode(nums[mid])
        node.left=sortedArrayToBST(nums.slice(0,mid))
        node.right=sortedArrayToBST(nums.slice(mid+1,nums.length))
        return node
}
~~~
