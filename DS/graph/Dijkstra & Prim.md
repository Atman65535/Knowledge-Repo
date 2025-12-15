# Dijkstra's Algorithm

Used to find **the shorttest paths** from a **single source node** to all other nodes in a graph with **non-negative weights**

### Key Concept: Single-Source Shortest Path

Greedily selecting the unvisited node with the smallest known distance from the starting node and then update the distance of its neighbors.

## Work Flow
1. Initialization 
	- Set distance to the source node as **0**
	- Set distance to all other nodes as infinity.
	- Mark all nodes as unvisited.
2. Iteration: while there is unvisited nodes.
	- Select the unvisited node u with the **smallest current distance**
	- Mark u as visited.
	- For each neibor v of u:
		- Calculate potential new distance to v: $new\_dist = dist[u] + weight(u, v)$.
		- if new distance is smaller, update it. 
3. Result: distance array will contains the shortest distance from source to every other node.

>[!tip] Shortest Path Comes from Visit
>When you choose which point to start, you choose next visited node, whose shortest path is certain.
>Think: if not, then there will be another node distance + weight < current minimum. weight >= 0, then fake.

# Trace Track

Track the prior node of each node. When update one node, update its prior pointer.

# Prim's Algorithm

prim's algorithm is used to find a Minimun Spanning Tree for a connected, weighted undirected graph.

### Key Concept: Minimun Spanning Tree

An MST is a subgraph that connects all the vertices together, without any cycles, and with the minimum possible total sum of edge weights.
<center> Not minimum path with weights </center>

## How it Works
1. Initalization:
	- Start with any arbitray node (vertex) as the initial tree.
	- Keep track of the minimum weight that connects each node to the growing tree. 
2. Iteration:
	- Select the edge with the **minimum weight** that connects a node in the currnet MST to a node not yet in the MST.
3. Result: The set of selected edges forms the MST.


