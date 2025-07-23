# Implement Trie

## Explanation

1. Initiate an empty dictionary to start with
2. When inserting a word, we need to make sure the last node has a terminator to signify that some word ends here
3. When searching you need to going down the tree.
    - If at any point you couldn't find the key in the tree, immediately return False i.e the word is not there
    - If we were able to traverse until the last character, return True if the last character has a "end" = True terminator key
4. For Prefix, you just need to traverse till the last char in the word. and if at any point the child node wasn't there, means there's no single word with that prefix

## Code
```python
class Trie:

    def __init__(self):
        self.trie = {}
        

    def insert(self, word: str) -> None:
        trie = self.trie
        for char in word:
            # if the key exists
            if char in trie:
                trie = trie[char]
            else:
                trie[char] = {}
                trie = trie[char]
        trie['end'] = True

    def search(self, word: str) -> bool:
        trie = self.trie
        for char in word:
            if char in trie:
                trie = trie[char]
            else:
                return False
        if 'end' in trie and trie['end'] == True:
            return True
        return False
        

    def startsWith(self, prefix: str) -> bool:
        trie = self.trie
        for char in prefix:
            if char in trie:
                trie = trie[char]
            else:
                return False
        return True
```