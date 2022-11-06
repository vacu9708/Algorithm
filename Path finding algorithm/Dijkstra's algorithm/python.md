~~~python
import heapq
INF=10_000_001
GRAPH_SIZE=10
# Make the adjacency list (initilization)
adjacencies=[[] for i in range(GRAPH_SIZE)]
weight_table=[INF for i in range(GRAPH_SIZE)]
already_shortests=[False for i in range(GRAPH_SIZE)]
def add_path(node1,node2,weight):
    adjacencies[node1].append((node2, weight))
    adjacencies[node2].append((node1, weight))
def dijkstra(start, shortest_paths):
    pq=[] # priority queue
    heapq.heappush(pq,(0,start))
    # Pop from pq and then update and push nodes connected to the popped node.
    while len(pq):
        weight,node=heapq.heappop(pq)
        if already_shortests[node]:
            continue
        already_shortests[node]=True
        for next_node in adjacencies[node]:
            if already_shortests[next_node[0]]:
                continue
            # Update if better path
            new_weight=weight+next_node[1]
            if new_weight<weight_table[next_node[0]]:
                weight_table[next_node[0]]=new_weight
                shortest_paths[next_node[0]]=shortest_paths[node]+[next_node[0]]
                heapq.heappush(pq,(new_weight,next_node[0]))


add_path(0, 1, 5)
add_path(1, 2, 5)
add_path(0, 2, 6)
add_path(0, 9, 14)
add_path(0, 8, 7)
add_path(8, 9, 15)
add_path(8, 7, 8)
add_path(1, 3, 4)
add_path(3, 2, 3)
add_path(3, 4, 6)
add_path(2, 4, 10)
add_path(4, 5, 8)
add_path(2, 5, 11)
add_path(2, 9, 5)
add_path(9, 5, 6)
add_path(9, 6, 4)
add_path(5, 6, 7)
add_path(7, 6, 3)

start=0
shortest_paths=[[] for i in range(GRAPH_SIZE)]
shortest_paths[start]=[start]
dijkstra(0, shortest_paths)
for i in range(len(shortest_paths)):
    print(f'from {start} to {i}: ', end='')
    for node in shortest_paths[i]:
        print(f'{node}->',end='')
    print('')
~~~

## Using hashmaps
~~~python
import heapq
INF=10_000_001
# Make the adjacency list (initilization)
adjacencies={}
weight_table={}
already_shortests={}
def add_path(node1,node2,weight):
    if not node1 in adjacencies:
        adjacencies[node1]=[(node2, weight)]
        weight_table[node1]=INF
        already_shortests[node1]=False
    if not node2 in adjacencies:
        adjacencies[node2]=[(node1, weight)]
        weight_table[node2]=INF
        already_shortests[node2]=False
    if node1 in adjacencies and node2 in adjacencies:
        adjacencies[node1].append((node2, weight))
        adjacencies[node2].append((node1, weight))
def dijkstra(start, shortest_paths):
    pq=[] # priority queue
    heapq.heappush(pq,(0,start))
    # Pop from pq and then update and push nodes connected to the popped node.
    while len(pq):
        weight,node=heapq.heappop(pq)
        if already_shortests[node]:
            continue
        already_shortests[node]=True
        for next_node in adjacencies[node]:
            if already_shortests[next_node[0]]:
                continue
            # Update if better path
            new_weight=weight+next_node[1]
            if new_weight<weight_table[next_node[0]]:
                weight_table[next_node[0]]=new_weight
                shortest_paths[next_node[0]]=shortest_paths[node]+[next_node[0]]
                heapq.heappush(pq,(new_weight,next_node[0]))


add_path(0, 1, 5)
add_path(1, 2, 5)
add_path(0, 2, 6)
add_path(0, 9, 14)
add_path(0, 8, 7)
add_path(8, 9, 15)
add_path(8, 7, 8)
add_path(1, 3, 4)
add_path(3, 2, 3)
add_path(3, 4, 6)
add_path(2, 4, 10)
add_path(4, 5, 8)
add_path(2, 5, 11)
add_path(2, 9, 5)
add_path(9, 5, 6)
add_path(9, 6, 4)
add_path(5, 6, 7)
add_path(7, 6, 3)
start=0
shortest_paths={start: [start]}
dijkstra(0, shortest_paths)
for key in shortest_paths:
    print(f'from {start} to {key}: ', end='')
    for node in shortest_paths[key]:
        print(f'{node}->',end='')
    print('')
~~~
