# Dijikstra's algorithm
>Dijkstra's algorithm is an algorithm for finding the shortest distances and paths between nodes in a graph, which may represent, for example, road networks.<br>
>It differs from the minimum spanning tree because the shortest distance between two vertices might not include all the vertices of the graph.

## Working process
>Shortest paths are found by visiting the nearest path that hasn't been visited and comparing old paths with new paths and updating the weight table.
<br>The weight table has information of shortest distances.

## Graph in the code
![Graph for dijikstra](https://user-images.githubusercontent.com/67142421/149639512-b50303aa-c579-45f6-9be7-21d48046626e.png)

## Using priority queue(This is the most efficient and useful)
>In the other methods, linear search is performed to find min vertex, which takes **O(n^2)**.<br>
>Instead, priority queue can be used to reduce the time taken for linear search to **O(logn)**

### Code to skip already shortest paths that are in the priority queue
~~~c++
if (already_shortest[current_vertex] == true) // If the path is already the shortest path, continue
	continue;
already_shortest[current_vertex] = true;
//if (weight_table[current_vertex] < current_weight) // If there's the shortest path to this vertex, continue (the same function as right above)
	//continue;
~~~
### Example picture of this case
Vertex 3 is processed twice, which should be prevented.

![image](https://user-images.githubusercontent.com/67142421/200169241-76460bf5-e714-4f40-9267-91f76dc31a78.png)

---
~~~c++
#include <iostream>
#include <vector>
#include <string>
#include <queue>
using namespace std;

const unsigned int INF = 987654321;
const char GRAPH_SIZE = 10;

class Path {
public:
	unsigned int to;
	unsigned int weight;
	Path(unsigned int to, unsigned int weight) {
		this->to = to;
		this->weight = weight;
	}
	bool const operator<(Path path) const {
		return this->weight > path.weight;
	}
};

vector<vector<Path>> graph(GRAPH_SIZE); // Adjacent list

void add_edge(int vertex1, int vertex2, int weight) {
	graph[vertex1].push_back(Path(vertex2, weight));
	graph[vertex2].push_back(Path(vertex1, weight));
}

vector<int> weight_table(GRAPH_SIZE, INF);
bool already_shortest[GRAPH_SIZE]; // All the paths where already_shortest == true are shorter than paths where already_shortest == false.
string shortest_paths[GRAPH_SIZE];

void dijkstra(int start) {
	// Initialize weights and shortest paths
	weight_table[start] = 0;
	shortest_paths[start] = to_string(start);
	//-----
	priority_queue<Path, vector<Path>, less<Path>> pq;
	pq.push(Path(start, 0));

	// Update.
	while(pq.empty() == false) {
		int current_vertex = pq.top().to;
		int current_weight = pq.top().weight;
		pq.pop();
		// Code to skip old paths in the priority queue
		if (already_shortest[current_vertex] == true) // If the path is already the shortest path
			continue;
		already_shortest[current_vertex] = true;
		
		for (int i = 0; i < graph[current_vertex].size(); i++) {
			if (already_shortest[graph[current_vertex][i].to] == true) // If the path is already the shortest path
				continue;

			int weight_of_new_path = current_weight + graph[current_vertex][i].weight; // new path
			// Update weight table and shortest path if the new path is better than the old path
			if (weight_of_new_path < weight_table[graph[current_vertex][i].to]) {
				weight_table[graph[current_vertex][i].to] = weight_of_new_path;
				shortest_paths[graph[current_vertex][i].to] = shortest_paths[current_vertex] + " -> " + to_string(graph[current_vertex][i].to);
				pq.push(Path(graph[current_vertex][i].to, weight_of_new_path));
			}
		}
	}
}

void print_result(int start) {
	cout << "Weight table : ";
	for (int i = 0; i < GRAPH_SIZE; i++)
		cout << weight_table[i] << " ";

	cout << "\n\n" << "-----Shortest paths" << "\n";
	for (int to = 0; to < GRAPH_SIZE; to++)
		cout << "From " << start << " to " << to << " : " << shortest_paths[to] << "\n";
}

int main(void) {
	add_edge(0, 1, 5);
	add_edge(1, 2, 5);
	add_edge(0, 2, 6);
	add_edge(0, 9, 14);
	add_edge(0, 8, 7);
	add_edge(8, 9, 15);
	add_edge(8, 7, 8);
	add_edge(1, 3, 4);
	add_edge(3, 2, 3);
	add_edge(3, 4, 6);
	add_edge(2, 4, 10);
	add_edge(4, 5, 8);
	add_edge(2, 5, 11);
	add_edge(2, 9, 5);
	add_edge(9, 5, 6);
	add_edge(9, 6, 4);
	add_edge(5, 6, 7);
	add_edge(7, 6, 3);

	int start = 0;
	dijkstra(start);
	print_result(start);
}
~~~
## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149639505-ae12585a-fa9c-41b6-a996-2a0d154a89d1.png)

## Using adjacent list
~~~c++
#include <iostream>
#include <vector>
#include <string>
using namespace std;

unsigned int INF = 987654321;
const char GRAPH_SIZE = 10;

class Path {
public:
	unsigned int to;
	unsigned int weight;
	Path(unsigned int to, unsigned int weight) {
		this->to = to;
		this->weight = weight;
	}
};

vector<vector<Path>> graph(GRAPH_SIZE); // Adjacent list

void add_edge(int vertex1, int vertex2, int weight) {
	graph[vertex1].push_back(Path(vertex2, weight));
	graph[vertex2].push_back(Path(vertex1, weight));
}

vector<int> weight_table(GRAPH_SIZE, INF);
bool already_shortest[GRAPH_SIZE]; // All the paths where already_shortest == true are shorter than paths where already_shortest == false.
string shortest_paths[GRAPH_SIZE];

int next_nearest_vertex() { // Find the best vertex to go that hasn't been visited (Can be more efficient by putting the weight table into a priority queue)
	int min_weight = INF, vertex_to_visit = 0;
	for (int i = 0; i < GRAPH_SIZE; i++)
		if (already_shortest[i] == false && weight_table[i] < min_weight) {
			min_weight = weight_table[i]; // Update current minimum
			vertex_to_visit = i;
		}

	return vertex_to_visit;
}

void dijkstra(int start) {
	// Initialize
	weight_table[start] = 0; // The path from start to start takes 0 weight
	shortest_paths[start] = to_string(start);
	//-----
	// Update. All the shortest paths from start vertex have to be found to know one shortest path.
	for (int i = 0; i < GRAPH_SIZE; i++) {
		int current_vertex = next_nearest_vertex();
		already_shortest[current_vertex] = true;
		for (int j = 0; j < graph[current_vertex].size(); j++) {
			if (already_shortest[graph[current_vertex][j].to] == true) // If the path is already the shortest path, continue
				continue;

			int weight_of_new_path = weight_table[current_vertex] + graph[current_vertex][j].weight; // new path
			// Update weight table and shortest path if the new path is better than the old path
			if (weight_of_new_path < weight_table[graph[current_vertex][j].to]) {
				weight_table[graph[current_vertex][j].to] = weight_of_new_path;
				shortest_paths[graph[current_vertex][j].to] = shortest_paths[current_vertex] + " -> " + to_string(graph[current_vertex][j].to);
			}
			//-----
		}
	}
	//-----
}

void print_result(int start) {
	cout << "Weight table : ";
	for (int i = 0; i < GRAPH_SIZE; i++)
		cout << weight_table[i] << " ";

	cout << "\n\n" << "-----Shortest paths" << "\n";
	for (int to = 0; to < GRAPH_SIZE; to++)
		if (start != to)
			cout << "From " << start << " to " << to << " : " << shortest_paths[to] << "\n";
}

int main(void) {
	add_edge(0, 1, 5);
	add_edge(1, 2, 5);
	add_edge(0, 2, 6);
	add_edge(0, 9, 14);
	add_edge(0, 8, 7);
	add_edge(8, 9, 15);
	add_edge(8, 7, 8);
	add_edge(1, 3, 4);
	add_edge(3, 2, 3);
	add_edge(3, 4, 6);
	add_edge(2, 4, 10);
	add_edge(4, 5, 8);
	add_edge(2, 5, 11);
	add_edge(2, 9, 5);
	add_edge(9, 5, 6);
	add_edge(9, 6, 4);
	add_edge(5, 6, 7);
	add_edge(7, 6, 3);

	int start = 0;
	dijkstra(start);
	print_result(start);
}
~~~

## Using adjacent matrix (The most inefficient)
~~~C++
#include <iostream>
#include <vector>
#include <string>
using namespace std;

unsigned int INF = 987654321;
const char GRAPH_SIZE = 10;

vector<vector<int>> graph(GRAPH_SIZE, vector<int>(GRAPH_SIZE)); // Adjacent matrix
//int graph[GRAPH_SIZE][GRAPH_SIZE]; // The same as above

void add_edge(int vertex1, int vertex2, int weight) {
	graph[vertex1][vertex2] = weight;
	graph[vertex2][vertex1] = weight;
}

int weight_table[GRAPH_SIZE];
bool already_shortest[GRAPH_SIZE]; // All the paths where already_shortest == true are shorter than paths where already_shortest == false.
string shortest_paths[GRAPH_SIZE];

// Find the next vertex that hasn't been visited and is nearest from the start vertext 
// (Can be more efficient by putting the weight table into a priority queue)
int next_nearest_vertex() {
	int min_weight = INF, vertex_to_visit = 0;
	for (int i = 0; i < GRAPH_SIZE; i++)
		if (already_shortest[i] == false && weight_table[i] < min_weight) {
			min_weight = weight_table[i]; // Update current minimum
			vertex_to_visit = i;
		}

	return vertex_to_visit;
}

void dijkstra(int start) {
	// Initialize weights and shortest paths
	already_shortest[start] = true;
	weight_table[start] = 0;
	
	for (int to = 0; to < GRAPH_SIZE; to++) {
		weight_table[to] = graph[start][to];

		if (start != to && graph[start][to] != INF) // Initialize available paths
			shortest_paths[to] = to_string(start) + " -> " + to_string(to);
	}

	// Update.
	for (int i = 0; i < GRAPH_SIZE; i++) {
		int current_vertex = next_nearest_vertex();
		already_shortest[current_vertex] = true; // The path to current_vertex is confirmed as the shortest
		for (int to = 0; to < GRAPH_SIZE; to++) { // Update vertices connected to the current vertex
			if (already_shortest[to] == true) // Not necessary because if the path is already shortest, it won't be updated below.
				continue;

			// Update weight table and shortest path if the new path is better than the old path
			int weight_of_new_path = weight_table[current_vertex] + graph[current_vertex][to]; // new path
			if (weight_of_new_path < weight_table[to]) {
				weight_table[to] = weight_of_new_path;
				shortest_paths[to] = shortest_paths[current_vertex] + " -> " + to_string(to);
			}
		}
	}
}

void print_result(int start) {
	cout << "Weight table : ";
	for (int i = 0; i < GRAPH_SIZE; i++)
		cout << weight_table[i] << " ";

	cout << "\n\n" << "-----Shortest paths" << "\n";
	for (int to = 0; to < GRAPH_SIZE; to++)
		if (start != to)
			cout << "From " << start << " to " << to << " : " << shortest_paths[to] << "\n";
}

int main(void) {
	for (int i = 0; i < GRAPH_SIZE; i++) // Intialize the graph with infinity
		for (int j = 0; j < GRAPH_SIZE; j++)
			i == j ? graph[i][j] = 0 : graph[i][j] = INF;

	add_edge(0, 1, 5);
	add_edge(1, 2, 5);
	add_edge(0, 2, 6);
	add_edge(0, 9, 14);
	add_edge(0, 8, 7);
	add_edge(8, 9, 15);
	add_edge(8, 7, 8);
	add_edge(1, 3, 4);
	add_edge(3, 2, 3);
	add_edge(3, 4, 6);
	add_edge(2, 4, 10);
	add_edge(4, 5, 8);
	add_edge(2, 5, 11);
	add_edge(2, 9, 5);
	add_edge(9, 5, 6);
	add_edge(9, 6, 4);
	add_edge(5, 6, 7);
	add_edge(7, 6, 3);

	int start = 0;
	dijkstra(start);
	print_result(start);
}
~~~
