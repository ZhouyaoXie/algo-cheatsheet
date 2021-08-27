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

#### BFS with Backtracking

#### Kahn's Algorithm [reference](https://www.youtube.com/watch?v=cIBFEhD77b4)

Intuition: recursively remove nodes with no dependencies (no incoming edges) from the graph, add the node to the result, until there are no nodes to process. If there are still nodes unvisited, a cycle is detected.

Specifications:
- Initialize a queue to store nodes to be processed. 
- Use an array or hashmap to keep track of the indegree of each vertex. Once a vertex has indegree of 0, add the vertex to the queue. Each time a node u is removed, decrease 1 indegree for all v s.t. u->v.
