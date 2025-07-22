# Pacific atlantic water flow

## Explanation

### Work in greedy way
1. Go from boundaries to inside the island
2. If the current cell less than next cell, means the water cal flow from next cell to current cell
3. Iterate for the pacific island first and mark all the cells we can flow to with p
4. Iterate for the atlantic island and mark all the cells we can flow to with a
5. If there's already 'p' in the cell while doing 'a' then mark that cell as 'x' i.e can flow in both oceans
6. Now iterate the result array and return the cells with 'x'


## Code
```python
class Solution:
    def is_pacific(self, x, y):
        return x == 0 or y == 0
    def is_atlantic(self, x, y):
        return x == len(self.heights)-1 or y == len(self.heights[0])-1

    def traverse(self, row, col, prev, current):
        if row < 0 or col < 0 or row >= self.rows or col >= self.cols:
            return
        
        r, c = prev
        if self.heights[r][c] > self.heights[row][col]:
            return

        if (row, col) in self.visited:
            return

        self.visited.add((row, col))

        if self.hg[row][col] == 'x':
            return

        if current == 'p':
            if self.hg[row][col] == 'a':
                self.hg[row][col] = 'x'
            else:
                self.hg[row][col] = 'p'
        elif current == 'a':
            if self.hg[row][col] == 'p':
                self.hg[row][col] = 'x'
            else:
                self.hg[row][col] = 'a'
        
        
        self.traverse(row+1, col, (row, col), current)
        self.traverse(row-1, col, (row, col), current)
        self.traverse(row, col+1, (row, col), current)
        self.traverse(row, col-1, (row, col), current)


    def pacificAtlantic(self, heights: List[List[int]]) -> List[List[int]]:
        self.rows, self.cols = len(heights), len(heights[0])

        self.heights = heights
        self.hg = [[x for x in y] for y in heights]
        self.pacific = set()
        self.atlantic = set()


        self.visited = set()
        for i in range(self.rows):
            for j in range(self.cols):
                if self.is_pacific(i, j):
                    self.traverse(i, j, (i, j), 'p')
        
        self.visited = set()
        for i in range(self.rows):
            for j in range(self.cols):
                if self.is_atlantic(i, j):
                    self.traverse(i, j, (i, j),'a')
        
        output = []
        for i in range(self.rows):
            for j in range(self.cols):
                if self.hg[i][j] =='x':
                    output.append([i, j])
        
        return output
```