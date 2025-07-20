# Number of islands

## Explanation

1. Start iterating the matrix
2. If at any point you encounter the "1", then start traversing from that path
3. Traverse all the neighbours (not diagonally) and mark those as visited
4. Continue the main iteration
5. Return the number of times we had to iterate / traverse

## Code
```python
class Solution:
    def traverse(self, row, col, parent):
        if row < 0 or col < 0 or row >= self.rows or col >= self.cols or (row, col) in self.visited or self.grid[row][col] == "0":
            return
        
        self.visited.add((row, col))
        self.traverse(row+1, col, parent)
        self.traverse(row-1, col, parent)
        self.traverse(row, col+1, parent)
        self.traverse(row, col-1, parent)
        

    def numIslands(self, grid: List[List[str]]) -> int:
        self.rows, self.cols = len(grid), len(grid[0])
        self.grid = grid

        self.islands = 0
        self.visited = set()

        for i in range(self.rows):
            for j in range(self.cols):
                if grid[i][j] == "1" and (i, j) not in self.visited:
                    self.traverse(i, j, (i, j))
                    self.islands += 1
            
        
        return self.islands
```