## Example Question & Solution

Example question: Leetcode 200. Number of Islands

```python
# deque is short for doubly linked queue, here we just use it as a normal queue
# refer to this doc to understand deque: https://docs.python.org/3/library/collections.html#collections.deque
from collections import deque

class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        
        # edge case
        if len(grid) == 0: return
        
        # number of islands
        res = 0
        
        m, n = len(grid), len(grid[0])
        
        # iterate through the matrix once to collect all 1's
        unvisited = set()
        for i in range(m):
            for j in range(n):
                if grid[i][j] == '1':
                    unvisited.add((i, j))
        
        # basic idea: continue looping until we've visited every element in `unvisited`
        while len(unvisited) > 0:
            
            # initiate a queue that contains the first element in `unvisited` 
            # because we would remove (x, y) within the nested while loop
            # we need to add (x, y) back to the set after first popping it
            x, y = unvisited.pop()
            q = deque([(x,y)])
            unvisited.add((x, y))
            
            # basic idea: continue looping until we've visited every element that connects with cell (x, y)
            while len(q) > 0:
                
                # pop the first element in the queue
                x, y = q.popleft()

                # remove (x, y) from `unvisited` 
                unvisited.remove((x, y))
                
                # check neighboring cells in four directions: up, down, left, right
                for dx, dy in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
                    new_x, new_y = x + dx, y + dy
                    
                    # we add a neighboring cell to the queue only if the following conditions are met:
                    # 1. the cell is a valid cell (coordinates are in the range 0~m-1, 0~n-1)
                    # 2. the cell is a land cell
                    # 3. the cell has not been visited before
                    # 4. the cell has not been added to the queue yet
                    if new_x >= 0 and new_x < m and new_y >= 0 and new_y < n \
                        and grid[new_x][new_y] == '1' \
                        and (new_x, new_y) in unvisited \
                        and (new_x, new_y) not in q:
                        
                        # add the cell to queue to be visited later if all four conditions are met
                        q.append((new_x, new_y))
                        
            # if the queue is empty, we've visited all cells in a connected component (aka an island), so we increment `res` by 1
            res += 1
            
        return res
```

## Additional Practices
- Task 1: Use a 3-by-3 matrix to walk through the code above step by step to make sure you understand what each of the two while loops are doing and what `unvisited` and `q` represent.
- Task 2: If the question asks "how many islands have an area larger than 2", how would you modify the code above to solve this question?
- Task 3: What if the question is "what is the area of the largest island"? How about "how many islands do not contain cells on the boundary"? Now do you see how BFS could be adapted to solve a series of graph problems?
- Task 4: Use the same algorithm to solve "130. Surrounded Regions", "785. Is Graph Bipartite?"
