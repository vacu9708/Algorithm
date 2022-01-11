~~~C++
#include <iostream>
#include <string>
using namespace std;

int INF = 1000000;
const char GRAPH_SIZE = 10;
int weight_table[GRAPH_SIZE];
bool visited[GRAPH_SIZE];

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

int find_vertex_to_visit() { // Find the best vertex to go that hasn't been visited (Can be more efficient putting weight table into priority queue)
	int min_weight = INF, vertex_to_visit = 0;
	for (int i = 0; i < GRAPH_SIZE; i++)
		if (!visited[i] && weight_table[i] < min_weight ) {
			min = weight_table[i]; // Update current minimum
			vertex_to_visit = i;
		}

	return vertex_to_visit;
}

void dijkstra(int start) {
	string shortest_paths[GRAPH_SIZE];

	// Initialize weights and shortest paths to go from start at the beginning
	visited[start] = true;
	for (int to = 0; to < GRAPH_SIZE; to++) {
		weight_table[to] = graph[start][to];
	
		if (graph[start][to] != INF && start != to)
			shortest_paths[to] = to_string(start) + " -> " + to_string(to);
	}
	
	// Update
	for (int i = 0; i < GRAPH_SIZE; i++) {
		int current_vertex = find_vertex_to_visit();
		visited[current_vertex] = true;
		for (int to = 0; to < GRAPH_SIZE; to++)
			if (!visited[to]) { // Visited vertices are already the best paths
				int weight_of_new_path = weight_table[current_vertex] + graph[current_vertex][to]; // new path
				if (weight_of_new_path < weight_table[to]) { // Update weight table and shortest path if the new path is better than the old path
					weight_table[to] = weight_of_new_path;
					shortest_paths[to] = shortest_paths[current_vertex] + " -> " + to_string(to);
				}
			}
	}
	
	// Print
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

dijkstra(0);
}
~~~
