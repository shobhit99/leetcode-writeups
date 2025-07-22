# Graph Valid tree

## Explanation
Points to remember
1. A tree will have edges = node - 1, you can directly eliminate this case
2. If there are multiple graphs (not connected) via any edge, you can use disjoint set here

# Remember Disjoint set is the KEYWORD here

> Alternative solution is to do DFS, you would create two way adjacency list of the edges, and start with one node and pass the current node as third param to the recursive function so that we don't go back to the same node again and in each call we will put the current node in the visited set and if at any point we encounter the node as visited, i.e cycle is there, so we exist and return false

## Code
```python
class Disjoint():
    def __init__(self, n):
        self.parent = {i:i for i in range(n)}
        self.rank = {i:0 for i in range(n)}
    
    def find(self, n):

        if self.parent[n] != n:
            self.parent[n] = self.find(self.parent[n])
        
        return self.parent[n]
    
    def union(self, x, y):
        root_x = self.find(x)
        root_y = self.find(y)

        if self.rank[root_x] > self.rank[root_y]:
            self.parent[root_y] = root_x
        else:
            self.parent[root_x] = root_y

            if self.rank[root_x] == self.rank[root_y]:
                self.rank[root_x] += 1

class Solution:
    def validTree(self, n: int, edges: List[List[int]]) -> bool:

        if n == 1:
            return True
        
        if len(edges) != n-1:
            return False

        disjoint = Disjoint(n)

        for edge in edges:
            a, b = edge
            disjoint.union(a, b)
        
        unique_parents = set()

        for i in range(n):
            parent = disjoint.find(i)
            unique_parents.add(parent)
        
        if len(unique_parents) > 1:
            return False
        
        return True
```