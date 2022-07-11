# [101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)
~~~javascript
var isSymmetric = function(root) {
    queue=[]
    let is_symmetric=true
    function left_first(node){
        if(!node){
            queue.push(null)
            return
        }
        queue.push(node.val)
        left_first(node.left)
        left_first(node.right)
    }
    function right_first(node){
        if(!node){
            if(queue.shift()!=null)
                is_symmetric=false
            return
        }
        if(queue.shift()!=node.val){
            is_symmetric=false
            return
        }
        right_first(node.right)
        right_first(node.left)
    }
    
    left_first(root.left)
    right_first(root.right)
    return is_symmetric
};
~~~
