# Dijikstra's algorithm
>Dijkstra's algorithm is an algorithm for finding the shortest paths between nodes in a graph, which may represent, for example, road networks.<br>
>It differs from the minimum spanning tree because the shortest distance between two vertices might not include all the vertices of the graph.

## Working process
>Shortest paths are found by comparing old paths with new paths and updating a weight table.

## Graph in this code
![Graph for dijikstra](https://user-images.githubusercontent.com/67142421/149639512-b50303aa-c579-45f6-9be7-21d48046626e.png)

~~~C++
#include <iostream>
#include <string>
using namespace std;

int INF = 987654321;
const char GRAPH_SIZE = 10;

//vector<vector<int>> graph(10);
int graph[GRAPH_SIZE][GRAPH_SIZE]; // Adjacent matrix

void add_edge(int vertex1, int vertex2, int weight) {
	graph[vertex1][vertex2] = weight;
	graph[vertex2][vertex1] = weight;

	/*if (vertex1 >= graph.size())
		graph.resize(vertex1);
	if (vertex2 >= graph[vertex1].size())
		graph[vertex1].resize(vertex2);*/
}

int weight_table[GRAPH_SIZE];
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
	// Initialize weights and shortest paths
	already_shortest[start] = true;
	for (int to = 0; to < GRAPH_SIZE; to++) {
		weight_table[to] = graph[start][to];

		if (start != to && graph[start][to] != INF) // Initialize available paths
			shortest_paths[to] = to_string(start) + " -> " + to_string(to);
	}
	//-----
	// Update. All the shortest paths from start vertex have to be found to know one shortest path.
	for (int i = 0; i < GRAPH_SIZE; i++) {
		int current_vertex = next_nearest_vertex();
		already_shortest[current_vertex] = true;
		for (int to = 0; to < GRAPH_SIZE; to++)
			if (already_shortest[to] == false) {
				int weight_of_new_path = weight_table[current_vertex] + graph[current_vertex][to]; // new path
				if (weight_of_new_path < weight_table[to]) { // Update weight table and shortest path if the new path is better than the old path
					weight_table[to] = weight_of_new_path;
					shortest_paths[to] = shortest_paths[current_vertex] + " -> " + to_string(to);
				}
			}
	}
	//-----
}

void print_result(int start){
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
## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149639505-ae12585a-fa9c-41b6-a996-2a0d154a89d1.png)

