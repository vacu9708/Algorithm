# [101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)

## First solution
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

## Better solution
~~~javascript
var isSymmetric = function(root) {
    function DFS(pointer1, pointer2){  
        if(!pointer1&&!pointer2) //If all the nodes are symmetric
            return true
        if((!pointer1||!pointer2) || (pointer1.val!=pointer2.val)) //If the 2 nodes are asymmetric
            return false
        //Return true if the tree is symmetric
        return DFS(pointer1.left, pointer2.right)&&DFS(pointer1.right, pointer2.left)
    }
    return DFS(root.left, root.right)
};
~~~
