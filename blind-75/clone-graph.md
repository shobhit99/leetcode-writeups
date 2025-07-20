# Clone Graph

## Explanation

1. Make a node
2. Memoize the cloned node in the dictionary
3. Recursively add the neighbors and if the neighbor is already cloned than return it from the dictionary
4. attach the neighor
5. return the cloned node

## Code
```python
from typing import Optional
class Solution:
    def __init__(self):
        self.cloned = {}
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:
        if not node:
            return None
        if node.val in self.cloned:
            return self.cloned[node.val]

        cloned_node =  Node(node.val)
        self.cloned[cloned_node.val] = cloned_node
        cloned_node.neighbors = [self.cloneGraph(ng) for ng in node.neighbors]
        return cloned_node
```