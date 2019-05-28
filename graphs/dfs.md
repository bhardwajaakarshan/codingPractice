# Depth First-Search

## Implementation of DFS on a Graph (Adjacency List)
Adjacency List:
An array of lists is used. Size of the array is equal to the number of vertices. Let the array be array[]. An entry array[i] represents the list of vertices adjacent to the ith vertex. This representation can also be used to represent a weighted graph. The weights of edges can be represented as lists of pairs. Following is adjacency list representation of the above graph.
```java
// Java program to print DFS traversal from a given given graph 
import java.io.*; 
import java.util.*; 

// This class represents a directed graph using adjacency list 
// representation 
class Graph { 
	private int V; // No. of vertices 

	// Array of lists for Adjacency List Representation 
	private LinkedList<Integer> adj[]; 

	// Constructor 
	Graph(int v) { 
		V = v; 
		adj = new LinkedList[v]; 
		for (int i=0; i<v; ++i) 
			adj[i] = new LinkedList(); 
	} 

	//Function to add an edge into the graph 
	void addEdge(int v, int w) { 
		adj[v].add(w); // Add w to v's list. 
	} 

	// A function used by DFS 
	void DFSUtil(int v,boolean visited[]) { 
		// Mark the current node as visited and print it 
		visited[v] = true; 
		System.out.print(v+" "); 

		// Recur for all the vertices adjacent to this vertex 
		Iterator<Integer> i = adj[v].listIterator(); 
		while (i.hasNext()) 
		{ 
			int n = i.next(); 
			if (!visited[n]) 
				DFSUtil(n, visited); 
		} 
	} 

	// The function to do DFS traversal. It uses recursive DFSUtil() 
	void DFS(int v) { 
		// Mark all the vertices as not visited(set as 
		// false by default in java) 
		boolean visited[] = new boolean[V]; 

		// Call the recursive helper function to print DFS traversal 
		DFSUtil(v, visited); 
	} 

	public static void main(String args[]) { 
		Graph g = new Graph(4); 

		g.addEdge(0, 1); 
		g.addEdge(0, 2); 
		g.addEdge(1, 2); 
		g.addEdge(2, 0); 
		g.addEdge(2, 3); 
		g.addEdge(3, 3); 

		System.out.println("Following is Depth First Traversal "+ 
						"(starting from vertex 2)"); 

		g.DFS(2); 
	} 
} 
// This code is contributed by Aakash Hasija 
```
Pros: Saves space O(|V|+|E|) . In the worst case, there can be C(V, 2) number of edges in a graph thus consuming O(V^2) space. Adding a vertex is easier.

Cons: Queries like whether there is an edge from vertex u to vertex v are not efficient and can be done O(V).

## Implementation using Adjacency Matrix
Adjacency Matrix:
Adjacency Matrix is a 2D array of size V x V where V is the number of vertices in a graph. Let the 2D array be adj[][], a slot adj[i][j] = 1 indicates that there is an edge from vertex i to vertex j. Adjacency matrix for undirected graph is always symmetric. Adjacency Matrix is also used to represent weighted graphs. If adj[i][j] = w, then there is an edge from vertex i to vertex j with weight w.
```java
public static void dfs(int i, int[][] graph, boolean[] visited) {
    if(!visited[i]){        
        visited[i] = true; // Mark node as "visited"
        System.out.print(i+1 + " ");

        for (int j = 0; j < graph[i].length; j++) {
            if (graph[i][j]==1 && !visited[j]) {   
                dfs(j, graph, visited); // Visit node
            }
        }
    }   
}

public static void main(String[] args) {
    // your matrix declare
    boolean [] visited = new boolean[10];
    int count = 0;
    for(int i = 0; i < graph.length; i++) {
        if(!visited[i]) {
            System.out.println("Component: " );
            dfs(i,graph,visited);
            ++count;
        }
    }
    System.out.println("Total number of Components: " + count);
}
```
Pros: Representation is easier to implement and follow. Removing an edge takes O(1) time. Queries like whether there is an edge from vertex ‘u’ to vertex ‘v’ are efficient and can be done O(1).

Cons: Consumes more space O(V^2). Even if the graph is sparse(contains less number of edges), it consumes the same space. Adding a vertex is O(V^2) time.

## DFS: Using iteration
```java
//An Iterative Java program to do DFS traversal from 
//a given source vertex. DFS(int s) traverses vertices 
//reachable from s. 

import java.util.*; 

public class GFG { 
	// This class represents a directed graph using adjacency 
	// list representation 
	static class Graph { 
		int V; //Number of Vertices 
		
		LinkedList<Integer>[] adj; // adjacency lists 
		
		//Constructor 
		Graph(int V) { 
			this.V = V; 
			adj = new LinkedList[V]; 
			
			for (int i = 0; i < adj.length; i++) 
				adj[i] = new LinkedList<Integer>(); 
			
		} 
		
		//To add an edge to graph 
		void addEdge(int v, int w) { 
			adj[v].add(w); // Add w to v’s list. 
		} 
		
		// prints all not yet visited vertices reachable from s 
		void DFS(int s) { 
			// Initially mark all vertices as not visited 
			Vector<Boolean> visited = new Vector<Boolean>(V); 
			for (int i = 0; i < V; i++) 
				visited.add(false); 
	
			// Create a stack for DFS 
			Stack<Integer> stack = new Stack<>(); 
			
			// Push the current source node 
			stack.push(s); 
			
			while(stack.empty() == false) { 
				// Pop a vertex from stack and print it 
				s = stack.peek(); 
				stack.pop(); 
				
				// Stack may contain same vertex twice. So 
				// we need to print the popped item only 
				// if it is not visited. 
				if(visited.get(s) == false) { 
					System.out.print(s + " "); 
					visited.set(s, true); 
				} 
				
				// Get all adjacent vertices of the popped vertex s 
				// If a adjacent has not been visited, then puah it 
				// to the stack. 
				Iterator<Integer> itr = adj[s].iterator(); 
				
				while (itr.hasNext()) { 
					int v = itr.next(); 
					if(!visited.get(v)) 
						stack.push(v); 
				} 
				
			} 
		} 
	} 
	
	// Driver program to test methods of graph class 
	public static void main(String[] args) 
	{ 
		// Total 5 vertices in graph 
		Graph g = new Graph(5); 
		
		g.addEdge(1, 0); 
		g.addEdge(0, 2); 
		g.addEdge(2, 1); 
		g.addEdge(0, 3); 
		g.addEdge(1, 4); 
			
		System.out.println("Following is the Depth First Traversal"); 
		g.DFS(0); 
	} 
} 
```
