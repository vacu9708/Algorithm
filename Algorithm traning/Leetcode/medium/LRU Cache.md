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
        val = self.dict.pop(key)  #Remove it first before inserting it at the end again
        self.dict[key] = val   
        return val        

    def put(self, key: int, value: int) -> None:
        if key in self.dict:    
            self.dict.pop(key)
        else:
            if len(self.dict) == self.capacity:
                del self.dict[next(iter(self.dict))] # 1st element of hashmap
        self.dict[key] = value
~~~

## hashmap + doubly linked list
