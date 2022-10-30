# Kruskal's minimum spanning tree
E : edge, V : vertice<br>
>A minimum spanning tree is a subset of an edge-weighted undirected graph that connects all the vertices together with the minimum number of edges and 
>minimum total edge weight, that is, **without any cycles**. <br>
>A minimum spanning tree has (V – 1) edges.

## Working process
>Greedy algorithm that uses the union find and sorting
1. Sort all edges in ascending order.
2. Pick an edge that has the smallest weight at the moment. 
3. Check if it forms a cycle with the spanning tree formed so far. If a cycle is not formed, include this edge. Else, discard it.
4. Repeat until there are (V-1) edges in the spanning tree. (until making the MST is finished). 

### Time complexity
Union find takes **O(1)**, Sorting takes **O(ElogV)**

## Graph used and the Minimum Spanning Tree made in this code
<img src="https://user-images.githubusercontent.com/67142421/149641825-299e573d-f986-4e29-8f4d-d85907f419a9.png" width="600" height="500">


~~~c++
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

class Edge {
public:
	int vertex1, vertex2, weight;
	bool in_MST = false;

	Edge(int vertex1, int vertex2, int weight) {
		this->vertex1 = vertex1;
		this->vertex2 = vertex2;
		this->weight = weight;
	}

	bool operator <(Edge& edge) { // For sorting
		return this->weight < edge.weight;
	}
};
vector<Edge> edges;
int graph_size = 7;
vector<int> connection_table(graph_size);

int get_parent(int vertex) {
	if (vertex == connection_table[vertex])
		return vertex;
	return get_parent(connection_table[vertex]);
}

bool is_cycle_made(int parent1, int parent2) { // Check if a cycle is made by checking if the 2 vertices have the same parent.
	if (parent1 == parent2) // They are in the same subset
		return true;
	else // They are in a different subset
		return false;
}

void Union(int parent1, int parent2) { // Do union of the 2 vertices so that they have the same parent.
	if (parent1 > parent2)
		connection_table[parent1] = parent2; // Change vertex1's connection
	else
		connection_table[parent2] = parent1;
}

void print_MST(vector<Edge> edges) {
	cout << "-----Minimum spanning tree" << endl;
	int total_weight = 0;
	for (Edge i : edges)
		if (i.in_MST) {
			cout << i.vertex1 << "--" << i.vertex2 << " (Weight : " << i.weight << ")\n";
			total_weight += i.weight;
		}
	cout << "Total weight of MST : " << total_weight;
}

void make_MST(vector<Edge>& edges) {
	sort(edges.begin(), edges.end()); // Sort in ascending order according to the weight of edges

	for (int i = 0; i < edges.size(); i++) {
		int parent1 = get_parent(edges[i].vertex1);
		int parent2 = get_parent(edges[i].vertex2);
		if (!is_cycle_made(parent1, parent2)) { // When they don't have the same parent, that is, when a cycle isn't made
			Union(parent1, parent2);
			edges[i].in_MST = true;
		}
		for (int i = 0; i < graph_size; i++) // To check connection table
			cout << connection_table[i] + 1 << " ";
		printf("\n");
	}

	print_MST(edges);
}

void print_graph(vector<Edge>& edges) {
	for (int i = 0; i < edges.size(); i++)
		cout << edges[i].vertex1 << "--" << edges[i].vertex2 << " (Weight : " << edges[i].weight << ")\n";
	cout << endl;
}

int main(void) {
	edges.push_back(Edge(1, 2, 35));
	edges.push_back(Edge(2, 3, 7));
	edges.push_back(Edge(0, 1, 29));
	edges.push_back(Edge(3, 6, 13));
	edges.push_back(Edge(3, 5, 23));
	edges.push_back(Edge(5, 6, 25));
	edges.push_back(Edge(1, 5, 34));
	edges.push_back(Edge(0, 4, 75));
	edges.push_back(Edge(4, 5, 53));

	print_graph(edges);

	for (int i = 0; i < graph_size; i++) // Initialize connection table
		connection_table[i] = i;

	make_MST(edges);
}
~~~

## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149641284-15e525f2-cef6-4a86-b44e-5729900ad735.png)
