# Kruskal's Algorithm for Minimum Spanning Tree (MST) using Python

# Aim
To implement Kruskal's algorithm in Python for finding the Minimum Spanning Tree (MST) of a connected, undirected, and weighted graph.

# Procedure
1. Begin with an understanding of Kruskal’s algorithm, which is a greedy algorithm used to find the MST of a graph.
2. Represent the graph as a list of edges with their corresponding weights.
3. Sort all the edges in non-decreasing order of their weights.
4. Initialize a disjoint set (union-find) data structure to detect cycles while adding edges.
5. Traverse the sorted edge list:
   - For each edge, check if including it forms a cycle using the union-find method.
   - If it does not form a cycle, include the edge in the MST.
6. Repeat until the MST includes (V - 1) edges, where V is the number of vertices in the graph.
7. Display the edges in the MST and compute the total cost.
# Program
```python
# Python program for Kruskal's algorithm to find
# Minimum Spanning Tree of a given connected,
# undirected and weighted graph
from collections import defaultdict
# Class to represent a graph
class Graph:
	def __init__(self, vertices):
		self.V = vertices # No. of vertices
		self.graph = [] # default dictionary
		# to store graph
	# function to add an edge to graph
	def addEdge(self, u, v, w):
		self.graph.append([u, v, w])
	# A utility function to find set of an element i
	# (uses path compression technique)
	def find(self, parent, i):
		if parent[i] == i:
			return i
		return self.find(parent, parent[i])
	# A function that does union of two sets of x and y
	# (uses union by rank)
	def union(self, parent, rank, x, y):
		xroot = self.find(parent, x)
		yroot = self.find(parent, y)
		# Attach smaller rank tree under root of
		# high rank tree (Union by Rank)
		if rank[xroot] < rank[yroot]:
			parent[xroot] = yroot
		elif rank[xroot] > rank[yroot]:
			parent[yroot] = xroot
		# If ranks are same, then make one as root
		# and increment its rank by one
		else:
			parent[yroot] = xroot
			rank[xroot] += 1
	# The main function to construct MST using Kruskal's
		# algorithm
	def KruskalMST(self):
		result = [] # This will store the resultant MST
		# An index variable, used for sorted edges
		i = 0
		# An index variable, used for result[]
		e = 0
		# Step 1: Sort all the edges in
		# non-decreasing order of their
		# weight. If we are not allowed to change the
		# given graph, we can create a copy of graph
		self.graph = sorted(self.graph,
							key=lambda item: item[2])
		parent = []
		rank = []
		# Create V subsets with single elements
		for node in range(self.V):
			parent.append(node)
			rank.append(0)
		# Number of edges to be taken is equal to V-1
		while e < self.V - 1:
			# Step 2: Pick the smallest edge and increment
			# the index for next iteration
			u, v, w = self.graph[i]
			i = i + 1
			x = self.find(parent, u)
			y = self.find(parent, v)
			# If including this edge doesn't
			# cause cycle, include it in result
			# and increment the indexof result
			# for next edge
			if x != y:
				e = e + 1
				result.append([u, v, w])
				self.union(parent, rank, x, y)
			# Else discard the edge
		minimumCost = 0
		print ("Edges in the constructed MST")
		for u, v, weight in result:
			minimumCost += weight
			print("%d -- %d == %d" % (u, v, weight))
		print("Minimum Spanning Tree" , minimumCost)

# Driver code
g = Graph(4)
g.addEdge(0, 1, 10)
g.addEdge(0, 2, 6)
g.addEdge(0, 3, 5)
g.addEdge(1, 3, 15)
g.addEdge(2, 3, 4)

# Function call
g.KruskalMST()
```

# Output

![image](https://github.com/user-attachments/assets/d6d6b104-4ac3-4974-96ff-f14a5d72d69c)


# Result
Kruskal's algorithm is successfully implemented using Python. The program identifies and displays the Minimum Spanning Tree by selecting the least weight edges while avoiding cycles. The final MST and its total minimum cost are displayed.
