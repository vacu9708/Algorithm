# [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

~~~javascript
var inorderTraversal = function(root) {
    let output=[]
    
    function dfs(node){
    if(!node)
        return
    
    dfs(node.left)
    output.push(node.val)
    dfs(node.right)
    }
    dfs(root)
    return output
};
~~~
