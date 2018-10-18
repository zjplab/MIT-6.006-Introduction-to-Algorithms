## Python version 
```python
# Python program for Bellman-Ford's single source 
# shortest path algorithm. 

from collections import defaultdict 

#Class to represent a graph 
class Graph: 

	def __init__(self,vertices): 
		self.V= vertices #No. of vertices 
		self.graph = [] # default dictionary to store graph 

	# function to add an edge to graph 
	def addEdge(self,u,v,w): 
		self.graph.append([u, v, w]) 
		
	# utility function used to print the solution 
	def printArr(self, dist): 
		print("Vertex Distance from Source") 
		for i in range(self.V): 
			print("%d \t\t %d" % (i, dist[i])) 
	
	# The main function that finds shortest distances from src to 
	# all other vertices using Bellman-Ford algorithm. The function 
	# also detects negative weight cycle 
	def BellmanFord(self, src): 

		# Step 1: Initialize distances from src to all other vertices 
		# as INFINITE 
		dist = [float("Inf")] * self.V 
		dist[src] = 0


		# Step 2: Relax all edges |V| - 1 times. A simple shortest 
		# path from src to any other vertex can have at-most |V| - 1 
		# edges 
		for i in range(self.V - 1): 
			# Update dist value and parent index of the adjacent vertices of 
			# the picked vertex. Consider only those vertices which are still in 
			# queue 
			for u, v, w in self.graph: 
				if dist[u] != float("Inf") and dist[u] + w < dist[v]: 
						dist[v] = dist[u] + w 

		# Step 3: check for negative-weight cycles. The above step 
		# guarantees shortest distances if graph doesn't contain 
		# negative weight cycle. If we get a shorter path, then there 
		# is a cycle. 

		for u, v, w in self.graph: 
				if dist[v]> dist[u]+w: 
						print "Graph contains negative weight cycle"
						return
						
		# print all distance 
		self.printArr(dist) 

g = Graph(5) 
g.addEdge(0, 1, -1) 
g.addEdge(0, 2, 4) 
g.addEdge(1, 2, 3) 
g.addEdge(1, 3, 2) 
g.addEdge(1, 4, 2) 
g.addEdge(3, 2, 5) 
g.addEdge(3, 1, 1) 
g.addEdge(4, 3, -3) 

#Print the solution 
g.BellmanFord(0) 

#This code is contributed by Neelam Yadav 
```

## C++ version 
```c++
// A C++ program for Bellman-Ford's single source 
// shortest path algorithm. 
#include <bits/stdc++.h> 
using namespace std;

class Graph{
public:
Graph(int v, int e):V(v), E(e), edge(vector<Edge>(e)){}
void ModifyEdge(int no, int src, int dest, int weight){
    edge[no].src=src;
    edge[no].dest=dest;
    edge[no].weight=weight;
}

void BellmanFord(int source){
//Inialization 
vector<int> dist(V, numeric_limits<int>::max());
dist[source]=0;

for(int i=1; i<= V-1; i++){
    for(auto &iter: edge){
        if(dist[iter.dest] > dist[iter.src]+ iter.weight)
            dist[iter.dest]=dist[iter.src]+ iter.weight;
    }
}// |V|-1 times of relaxation 

for(int j=0; j<E; j++){
    if(dist[ edge[j].dest]> dist[edge[j].src]+edge[j].weight )
    {cout<<"Error"<<endl; break; }
}
printArr(dist, V);
}

private:
int V; //# of vertices
int E; // # of edges 
struct Edge { int src; int dest; int weight; };
vector<Edge> edge;
// A utility function used to print the solution 
void printArr(vector<int> &dist, int n) 
{ 
	printf("Vertex Distance from Source\n"); 
	for (int i = 0; i < n; ++i) 
		printf("%d \t\t %d\n", i, dist[i]); 
} 

};




// Driver program to test above functions 
int main() 
{ 
	/* Let us create the graph given in above example */
	int V = 5; // Number of vertices in graph 
	int E = 8; // Number of edges in graph 
	Graph graph(V,E);
   

	// add edge 0-1 (or A-B in above figure) 
	 graph.ModifyEdge(0, 0,1,-1);

	// add edge 0-2 (or A-C in above figure) 
    graph.ModifyEdge(1, 0,2,4);

	// add edge 1-2 (or B-C in above figure) 

    graph.ModifyEdge(2, 1,2,3);
	// add edge 1-3 (or B-D in above figure) 
	graph.ModifyEdge(3, 1,3,2);

	// add edge 1-4 (or A-E in above figure) 
	graph.ModifyEdge(4, 1,4,2);

	// add edge 3-2 (or D-C in above figure) 
	graph.ModifyEdge(5, 3,2,5); 

	// add edge 3-1 (or D-B in above figure) 
	graph.ModifyEdge(6, 3,1,1);

	// add edge 4-3 (or E-D in above figure) 
	graph.ModifyEdge(7, 4,3,-3) ;

	graph.BellmanFord(0);

	return 0; 
} 
```
