# [LRU Cache](https://leetcode.com/problems/lru-cache/solutions/?orderBy=most_votes)
## Taking advantage of python dict (which does use a doubly linked list to maintain the order of the hashmap)
~~~python
class LRUCache:
    def __init__(self, capacity: int):
        self.dict = {}
        self.capacity = capacity   

    def get(self, key: int) -> int:
        if key not in self.dict:
            return -1
        val = self.dict.pop(key)
        self.dict[key] = val   
        return val        

    def put(self, key: int, value: int) -> None:
        if key not in self.dict:
            if len(self.dict) == self.capacity:
                del self.dict[next(iter(self.dict))] # 1st element of hashmap
        else:    
            del self.dict[key]
        self.dict[key] = value
~~~

## hashmap + doubly linked list
~~~python
class Node:
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.left = self.right = None

class Linked_list:
    def __init__(self):
        self.head=self.tail=None

    def append(self, node):
        if not self.head:
            self.head=node
            self.tail=self.head
            return
        self.tail.right=node
        node.left=self.tail
        self.tail=node

    def remove(self, node):
        if node.left:
            node.left.right=node.right
        if node.right:
            node.right.left=node.left
        if node==self.head:
            self.head=self.head.right
        if node==self.tail:
            self.tail=self.tail.left
        node.left=node.right=None

class LRUCache:
    def __init__(self, capacity):
        self.capacity=capacity
        self.map={}
        self.order_list=Linked_list()

    def get(self, key):
        if key not in self.map:
            return -1
        self.order_list.remove(self.map[key])
        self.order_list.append(self.map[key])
        return self.map[key].value

    def put(self, key, value):
        if key not in self.map:
            if len(self.map)==self.capacity:
                head=self.order_list.head
                del self.map[head.key]
                self.order_list.remove(head)
            node=Node(key, value)
            self.order_list.append(node)
            self.map[key]=node
        else:
            self.map[key].value=value
            self.order_list.remove(self.map[key])
            self.order_list.append(self.map[key])
~~~
