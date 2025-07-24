# Word search 2

## Explanation
1. Create a trie of all the input words
2. Start the dfs and pass the root trie as the argument
3. For each iteration check if the current cell (i,j) exists in the trie
4. if the trie.get(char, {}).get('#') is True which means the word is complete. then add it to the output
5. If yes, then navigate the neighbouring cells and pass the trie[char] as trie to that

Base condition
6. If the trie is None, return


## Code
```python
class Trie:
    def __init__(self):
        self.trie = {}
    
    def insert(self, word):
        trie = self.trie
        for char in word:
            if char in trie:
                trie = trie[char]
            else:
                trie[char] = {}
                trie = trie[char]
        trie['#'] = True
    
    def search(self, word):
        trie = self.trie
        for char in word:
            if char in trie:
                trie = trie[char]
            else:
                return False
        return trie.get('#')

class Solution:
    def traverse(self, row, col, trie, word):
        if row < 0 or col < 0 or row >= self.rows or col >= self.cols or self.board[row][col] == 0:
            return
        
        if not trie:
            return
        
        char = self.board[row][col]
        if char in trie:
            word =  word + char
            if trie.get(char, {}).get('#'):
                self.output.add(word)
            placeholder = self.board[row][col]
            self.board[row][col] = 0
            self.traverse(row+1, col, trie[char], word)
            self.traverse(row-1, col, trie[char], word)
            self.traverse(row, col+1, trie[char], word)
            self.traverse(row, col-1, trie[char], word)
            self.board[row][col] = placeholder

    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        self.board = board
        self.rows, self.cols = len(board), len(board[0])
        self.trie = Trie()
        self.output = set()

        if self.rows == self.cols == 1:
            if self.board[0][0] == words[0]:
                return [words[0]]

        for word in words:
            self.trie.insert(word)
        
        for i in range(self.rows):
            for j in range(self.cols):
                self.traverse(i, j, self.trie.trie, "")
        
        return list(self.output)
```