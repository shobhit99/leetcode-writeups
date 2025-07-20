# Word search

## Explanation - my solution
1. Iterate each element in the matrix
2. Check for the solution if the current iteration alphabet in matrix has words[0]
3. In the traverse logic, if the word[0] is there, we will traverse the neighbours and pass the reducred word
4. If at any point the word is empty that means we have completed the word

```python
class Solution:
    def traverse(self, row, col, word, visited):
        if row < 0 or col < 0 or row >= self.rows or col >= self.cols or (row, col) in visited: 
            return
        
        visited.append((row, col))

        if self.board[row][col] == word[0]:
            new_word = word[1:]
            if not new_word:
                self.found = True
                return
            self.traverse(row, col+1, word[1:], visited[:])
            self.traverse(row, col-1, word[1:], visited[:])
            self.traverse(row+1, col, word[1:], visited[:])
            self.traverse(row-1, col, word[1:], visited[:])
        

    def exist(self, board: List[List[str]], word: str) -> bool:
        self.rows, self.cols = len(board), len(board[0])
        self.board = board

        starting_word = word[0]

        for i in range(self.rows):
            for j in range(self.cols):
                self.visited = set()
                self.found = False
                if board[i][j] == starting_word:
                    self.traverse(i, j, word, [])
                    if self.found:
                        return True
        return False
```