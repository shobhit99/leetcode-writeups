# No of connected components in unidirected graph

## Explanation

Use Disjoint set and count the no of parents and return them

## Code

```python
class Disjoint():
    def __init__(self, n):
        self.parent = {i: i for i in range(n)}
        self.rank = {i: 0 for i in range(n)}

    def find(self, n):

        if self.parent[n] != n:
            self.parent[n] = self.find(self.parent[n])
        
        return self.parent[n]
    
    def union(self, x, y):
        x_root = self.find(x)
        y_root = self.find(y)

        if self.rank[x_root] > self.rank[y_root]:
            self.parent[y_root] = x_root
        else:
            self.parent[x_root] = y_root
        
            if self.rank[x_root] == self.rank[y_root]:
                self.rank[x_root] += 1


class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        if n == 1:
            return 1
        
        if n == 0:
            return 0

        disjoint = Disjoint(n)

        for edge in edges:
            a, b = edge
            disjoint.union(a, b)
        
        parents = set()
        for i in range(n):
            p = disjoint.find(i)
            parents.add(p)
        
        return len(parents)
```