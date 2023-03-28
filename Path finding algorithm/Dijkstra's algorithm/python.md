## Basic
~~~python
class Path:
    def __init__(self, dest, weight):
        self.dest=dest
        self.weight=weight

import heapq
def dijikstra(N, paths):
    # Make adjacency list
    adjacencies=[[] for i in range(N)]
    for path in paths:
        adjacencies[path[0]].append(Path(path[1], path[2]))
        adjacencies[path[1]].append(Path(path[0], path[2]))
    # Dijikstra
    INF=999999999
    weights=[INF for i in range(N)]
    #visited=[False for i in range(N)] # Optional
    pq=[(0,0)] # (weight, destination)
    while len(pq):
        curr=heapq.heappop(pq) # Location that hasn't been visited and is easiest to get to
        #if visited[curr[1]]: continue # Optional
        #visited[curr[1]]=True # Optional
        for path in adjacencies[curr[1]]:
            #if visited[path.dest]: continue # Optional
            # Update if new path is better
            new_path_weight=curr[0]+path.weight
            if new_path_weight<weights[path.dest]:
                weights[path.dest]=new_path_weight
                heapq.heappush(pq,(new_path_weight,path.dest))
    # Print
    print(f'weight table: {weights}')
    
paths=((0,1,5),(1,2,5),(0,2,6),(0,9,14),(0,8,7),(8, 9, 15),(8, 7, 8),(1, 3, 4),(3, 2, 3),(3, 4, 6),(2, 4, 10),(4, 5, 8),(2, 5, 11),(2, 9, 5),(9, 5, 6),(9, 6, 4),(5, 6, 7),(7, 6, 3))
dijikstra(len(paths), paths)
~~~

## Printing paths with recursion
~~~python
class Path:
    def __init__(self, dest, weight):
        self.dest=dest
        self.weight=weight

def find_path(path_table, destination):
    if destination==path_table[destination]:
        print(destination, end='->')
        return
    find_path(path_table, path_table[destination])
    print(destination, end='->')

import heapq
def dijikstra(N, paths):
    # Make adjacency list
    adjacencies=[[] for i in range(N)]
    for path in paths:
        adjacencies[path[0]].append(Path(path[1], path[2]))
        adjacencies[path[1]].append(Path(path[0], path[2]))
    # Dijikstra
    path_table=[i for i in range(N)]
    INF=999999999
    weights=[INF for i in range(N)]
    #visited=[False for i in range(N)] # Optional
    pq=[(0,0)] # (weight, destination)
    while len(pq):
        curr=heapq.heappop(pq) # Location that hasn't been visited and is easiest to get to
        #if visited[curr[1]]: continue # Optional
        #visited[curr[1]]=True # Optional
        for path in adjacencies[curr[1]]:
            #if visited[path.dest]: continue # Optional
            # Update if new path is better
            new_path_weight=curr[0]+path.weight
            if new_path_weight<weights[path.dest]:
                weights[path.dest]=new_path_weight
                path_table[path.dest]=curr[1]
                heapq.heappush(pq,(new_path_weight,path.dest))
    # Print
    print(f'weight table: {weights}')
    for destination in range(1, len(path_table)):
        print(destination, end=': ')
        find_path(path_table, destination)
        print()
    
paths=((0,1,5),(1,2,5),(0,2,6),(0,9,14),(0,8,7),(8, 9, 15),(8, 7, 8),(1, 3, 4),(3, 2, 3),(3, 4, 6),(2, 4, 10),(4, 5, 8),(2, 5, 11),(2, 9, 5),(9, 5, 6),(9, 6, 4),(5, 6, 7),(7, 6, 3))
dijikstra(10, paths)
~~~

# [Floyd warshall](https://github.com/vacu9708/Algorithm/blob/main/Algorithm%20traning/Programmers/level3/%ED%95%A9%EC%8A%B9%20%ED%83%9D%EC%8B%9C%20%EC%9A%94%EA%B8%88.md)
