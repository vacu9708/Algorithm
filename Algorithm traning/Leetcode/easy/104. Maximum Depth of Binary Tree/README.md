# [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
~~~javascript
var maxDepth = function(root) {
    let answer=0
    function dfs(node, level){
        if(!node)
            return
        if(level>answer)
            answer=level
        dfs(node.left, level+1)
        dfs(node.right, level+1)
    }
    dfs(root, 1)
    return answer
};
~~~
