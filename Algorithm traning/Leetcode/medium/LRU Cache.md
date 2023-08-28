# [LRU Cache](https://leetcode.com/problems/lru-cache/solutions/?orderBy=most_votes)
An LRU (Least Recently Used) cache is a data structure that is used to store a limited number of items with a fast access time.<br>
The cache is designed to evict the least recently used items when the cache reaches its capacity.

## Taking advantage of python dict (which does use a doubly linked list to maintain the order of the hashmap)
~~~python
class LRUCache:
    def __init__(self, capacity: int):
        self.dict = {}
        self.capacity = capacity   

    def get(self, key: int) -> int:
        if key not in self.dict: # Cache miss
            return -1
        # Cache hit
        val = self.dict.pop(key)
        self.dict[key] = val   
        return val        

    def put(self, key: int, value: int) -> None:
        if key not in self.dict: # Cache miss
            if len(self.dict) == self.capacity:
                del self.dict[next(iter(self.dict))] # 1st element of hashmap
        else: # Cache hit
            del self.dict[key]
        self.dict[key] = value
~~~

## hashmap + doubly linked list makes an ordered hashmap
![image](https://github.com/vacu9708/Algorithm/assets/67142421/cb8be100-206b-4121-a9bf-8a60fff9cd45)
[LRU.cache.pptx](https://github.com/vacu9708/Algorithm/files/12456576/LRU.cache.pptx)

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
        node.left, node.right=self.tail, None
        self.tail=node

    def remove(self, node):
        # Change the connection
        if node.left:
            node.left.right=node.right
        if node.right:
            node.right.left=node.left
        # Change head or tail
        if node==self.head:
            self.head=self.head.right
        if node==self.tail:
            self.tail=self.tail.left
        #node.left=node.right=None

class LRUCache:
    def __init__(self, capacity):
        self.capacity=capacity
        self.map={}
        self.order=Linked_list()

    def get(self, key):
        if key not in self.map: # Cache miss
            return -1
        # Update
        self.order.remove(self.map[key])
        self.order.append(self.map[key])
        
        return self.map[key].value

    def put(self, key, value):
        if key not in self.map: # Cache miss
            if len(self.map)==self.capacity: # Cache full
                # Evict
                head=self.order.head
                del self.map[head.key]
                self.order.remove(head)
            # Add
            node=Node(key, value)
            self.order.append(node)
            self.map[key]=node
        else: # Cache hit
            self.map[key].value=value
            # Update
            self.order.remove(self.map[key])
            self.order.append(self.map[key])
~~~
