```
#include <iostream>
#include <vector>
#include <queue>
#include <utility>

using namespace std;

// An adjacency list. Each adjList[i] holds a all the friends of node i.
// The first int is the vertex of the friend, the second int is the edge weight.
vector< vector<pair<int, int> > > FormAdjList()
    {
    // Our adjacency list.
    vector< vector<pair<int, int> > > adjList;
    
    // We have 7 vertices, so initialize 7 rows.
    const int n = 7;
    
    for(int i = 0; i < n; i++)
        {
        // Create a vector to represent a row, and add it to the adjList.
        vector<pair<int, int> > row;
        adjList.push_back(row);
        }
    
    
    // Now let's add our actual edges into the adjacency list.
    // See the picture here: https://www.srcmake.com/uploads/5/3/9/0/5390645/spadjlist_orig.jpg
    
    adjList[0].push_back(make_pair(1, 2));
    adjList[0].push_back(make_pair(2, 3));
    
    adjList[1].push_back(make_pair(0, 2));
    adjList[1].push_back(make_pair(5, 1));
    
    adjList[2].push_back(make_pair(0, 3));
    adjList[2].push_back(make_pair(5, 2));
    
    adjList[3].push_back(make_pair(1, 4));
    adjList[3].push_back(make_pair(4, 1));
    adjList[3].push_back(make_pair(6, 2));
    
    adjList[4].push_back(make_pair(3, 1));
    adjList[4].push_back(make_pair(5, 2));
    adjList[4].push_back(make_pair(6, 1));
    
    adjList[5].push_back(make_pair(1, 1));
    adjList[5].push_back(make_pair(2, 2));
    adjList[5].push_back(make_pair(4, 2));
    adjList[5].push_back(make_pair(6, 2));
    
    adjList[6].push_back(make_pair(3, 2));
    adjList[6].push_back(make_pair(4, 1));
    adjList[6].push_back(make_pair(5, 2));
    
    // Our graph is now represented as an adjacency list. Return it.
    return adjList;
    }
    
// Given an Adjacency List, find all shortest paths from "start" to all other vertices.
vector<int> DijkstraSP(vector< vector<pair<int, int> > > &adjList, int &start)
    {
    cout << "\nGetting the shortest path from " << start << " to all other nodes.\n";
    vector<int> dist;
    
    // Initialize all source->vertex as infinite.
    int n = adjList.size();
    for(int i = 0; i < n; i++)
        {
        dist.push_back(1000000007); // Define "infinity" as necessary by constraints.
        }
        
    typedef pair<int, int> mypair;
    struct compare{
      bool operator() (const mypair &p1, const mypair &p2){
          return p1.second > p2.second ;
      }   
    };
    // Create a PQ.
    priority_queue<pair<int, int>, vector< pair<int, int> >, compare > pq;
    
    // Add source to pq, where distance is 0.
    pq.push(make_pair(start, 0));
    dist[start] = 0;
    
    // While pq isn't empty...
    while(pq.empty() == false)
        {
        // Get min distance vertex from pq. (Call it u.)
        int u = pq.top().first;
        pq.pop();
        
        // Visit all of u's friends. For each one (called v)....
        for(int i = 0; i < adjList[u].size(); i++)
            {
            int v = adjList[u][i].first;
            int weight = adjList[u][i].second;
            
            // If the distance to v is shorter by going through u...
            if(dist[v] > dist[u] + weight)
                {
                // Update the distance of v.
                dist[v] = dist[u] + weight;
                // Insert v into the pq. 
                pq.push(make_pair(v, dist[v]));
                }
            }
        }
    
    return dist;
    }
    
void PrintShortestPath(vector<int> &dist, int &start)
    {
    cout << "\nPrinting the shortest paths for node " << start << ".\n";
    for(int i = 0; i < dist.size(); i++)
        {
        cout << "The distance from node " << start << " to node " << i << " is: " << dist[i] << endl;
        }
    }
    
int main() 
    {
    cout << "Program started.\n";
    
    // Construct the adjacency list that represents our graph. 
    vector< vector<pair<int, int> > > adjList = FormAdjList();
    
    // Get a list of shortest path distances for node 0.
    int node = 0;
    vector<int> dist = DijkstraSP(adjList, node);
    
    // Print the list.
    PrintShortestPath(dist, node);
    
    cout << "Program ended.\n";
    
    return 0;
    }
```
