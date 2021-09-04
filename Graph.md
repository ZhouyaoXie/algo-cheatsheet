# TOC

- Disjoint Set
- DAG
- Topological Sort
- Shortest Path

### Disjoint Set

A data structure that stores connectivity info by keeping a hashmap storing {node: parent} pairs. Supports two operations:

- Union: when union two nodes u and v, need to choose one node as the parent node. If u is chosen, find the root of v, and update its parent to be u.
  - Optimization: union by rank. Keep track of the rank of each node, and when union, always choose the larger rank node to be the parent.
  - Time complexity: amortized average O(a(N)), where a(.) is the inverse Ackermann function, close to O(1) in practice. 
- Find: to check whether u and v are connected, check whether their root nodes are the same. Root node can be found by recursively going to the parent node until you reach a node whose parent is itself.
  - Optimization: path compression. When recursing upwards to find the root, also update the parent of each node on the path to be the root node.
  - Time complexity: amortized average O(a(N)).

My implementation of the optimized disjoint set data structure: [check this repo](https://github.com/ZhouyaoXie/DisjointSet)

### DAG

Directed, acyclic graphs. Trees are a special type of DAGs that satisfies a child has only one parent.

Common Applications:
- Course prerequisites ([Leetcode problem](https://leetcode.com/problems/course-schedule/))
- Program dependencies
- Assembly instructions

### Topological Sort

- Sort vertices in a DAG in an order such that if u->v, u appears before v.
- Topological orderings are not unique.
- Only DAGs have valid topological sort; a graph with cycles do not have valid topological sort.

#### DFS Via Backtracking

Intuition: for each unvisited node u, recursively visit each v s.t. there's an edge u->v. If v has been visited before, cycle detected; if v has no outgoing edges, return. u is appended to output after all v's have been visited.

#### Kahn's Algorithm [reference](https://www.youtube.com/watch?v=cIBFEhD77b4)

Intuition: recursively remove nodes with no dependencies (no incoming edges) from the graph, add the node to the result, until there are no nodes to process. If there are still nodes unvisited, a cycle is detected.

Specifications:
- Initialize a queue to store nodes to be processed. 
- Use an array or hashmap to keep track of the indegree of each vertex. Once a vertex has indegree of 0, add the vertex to the queue. Each time a node u is removed, decrease 1 indegree for all v s.t. u->v.

Time complexity: O(|E|+|V|)  

Space complexity: O(|E|+|V|)

### Shortest Path

#### Dijkstra's Algorithm

- Single-source shortest path problem
- Do not work with negative weights

Intuition:
- Keep a distance array for the shortest distance from start vertex s to node v. Intialize distances are `inf`.
- Keep a priority queue of (vertex, distance) pair.
- While priority queue is not empty, pop the shortest distance pair, update all relevant distances. Insert updated (vertex, distance) pair into the queue.
- Get the shortest path instead of just the shortest distance by also keeping a prev array.

Improvements:
- Stopping early is possible if the destination node is specified.
- Using an indexed priority queue instead of just simple priority queue to avoid duplicated nodes.

Time complexity: O((|V|+|E|)log(|V|)) = O(|E|log(|V|)) assuming |V| << |E|

Space complexity: O(|V|+|E|)
