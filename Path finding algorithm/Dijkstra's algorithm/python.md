
~~~python
import heapq
class Path:
    def __init__(self, dest, weight):
        self.dest=dest
        self.weight=weight

N=10
def dijikstra(adjacencies):
    INF=999999999
    weights=[INF for i in range(N)]
    weights[0]=0 # Start location's weight = 0
    pq=[(0,0)] # (weight, next_location)
    #visited=[False for i in range(N)]
    while pq:
        curr=heapq.heappop(pq) # Location that hasn't been visited and is easiest to get to
        # if visited[curr[1]]: continue
        # visited[curr[1]]=True
        for path in adjacencies[curr[1]]:
            # Update if new path is better
            new_path_weight=curr[0]+path.weight
            if new_path_weight<weights[path.dest]:
                weights[path.dest]=new_path_weight
                heapq.heappush(pq,(new_path_weight,path.dest))

    print(f'weight table: {weights}')

# Make adjacency list
paths=((0,1,5),(1,2,5),(0,2,6),(0,9,14),(0,8,7),(8, 9, 15),(8, 7, 8),(1, 3, 4),(3, 2, 3),(3, 4, 6),(2, 4, 10),(4, 5, 8),(2, 5, 11),(2, 9, 5),(9, 5, 6),(9, 6, 4),(5, 6, 7),(7, 6, 3))
adjacencies=[[] for i in range(N)] # <start, destination, weight>
for path in paths:
    adjacencies[path[0]].append(Path(path[1], path[2]))
    adjacencies[path[1]].append(Path(path[0], path[2]))
dijikstra(adjacencies)
~~~

## Printing paths recursively(union-find)
~~~python
import heapq
class Path:
    def __init__(self, dest, weight):
        self.dest=dest
        self.weight=weight

N=10
def dijikstra(adjacencies):
    shortest_routes=[i for i in range(N)] # index: destination, value: the node right before it
    INF=999999999
    weights=[INF for i in range(N)]
    weights[0]=0 # Start location's weight = 0
    pq=[(0,0)]
    while pq:
        curr=heapq.heappop(pq) # Location that hasn't been visited and is easiest to get to\
        for path in adjacencies[curr[1]]:
            new_path_weight=curr[0]+path.weight
            if new_path_weight<weights[path.dest]:
                weights[path.dest]=new_path_weight
                heapq.heappush(pq,(new_path_weight,path.dest))
                shortest_routes[path.dest]=curr[1]

    print_result(weights, shortest_routes)

# Rewind path to the destination to find the path
def find_path(paths, destination):
    if destination==paths[destination]:
        print(destination, end='->')
        return
    find_path(paths, paths[destination])
    print(destination, end='->')
    
def print_result(weights, paths):
    print(f'weight table: {weights}')
    for destination in range(1, len(paths)):
        print(destination, end=': ')
        find_path(paths, destination)
        print()

# Make adjacency list
paths=((0,1,5),(1,2,5),(0,2,6),(0,9,14),(0,8,7),(8, 9, 15),(8, 7, 8),(1, 3, 4),(3, 2, 3),(3, 4, 6),(2, 4, 10),(4, 5, 8),(2, 5, 11),(2, 9, 5),(9, 5, 6),(9, 6, 4),(5, 6, 7),(7, 6, 3))
adjacencies=[[] for i in range(N)]
for path in paths:
    adjacencies[path[0]].append(Path(path[1], path[2]))
    adjacencies[path[1]].append(Path(path[0], path[2]))
dijikstra(adjacencies)
~~~

# [Floyd warshall](https://github.com/vacu9708/Algorithm/blob/main/Algorithm%20traning/Programmers/level3/%ED%95%A9%EC%8A%B9%20%ED%83%9D%EC%8B%9C%20%EC%9A%94%EA%B8%88.md)
