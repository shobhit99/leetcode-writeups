# Design and add search words data structure

## Explanation
1. Create a wrapper function for search and pass the word and base trie tree to that function
2. In the wrapper function `_search`
    - If the char is .
        - Create a flag `Found` with `False` value
        - For each key in the trie
            - call the _search function again with the word[1:] and the subtree of that char and catch the output in Found
            - If the Found is True; return True
        - If the current char in word is not "."
            - Call the _search function with word[1:] and subtree of that char
        - If the current char is not in the current subtree
            - return False
3. Add the base conditions
    - If the word is empty and trie is there and that trie has only one key i.e 'end' as True i.e the word exists; return True
    - If the word is there and the trie only has 'end' key. that means the search input is > any word we have; return False;
    - else continue the function

## Code
```python
class WordDictionary:

    def __init__(self):
        self.trie = {}

    def addWord(self, word: str) -> None:
        trie = self.trie
        for character in word:
            if character in trie:
                trie = trie[character]
            else:
                trie[character] = {}
                trie = trie[character]
        trie['end'] = True
        
    def _search(self, word, trie):
        if word and len(trie.keys()) == 1 and 'end' in trie.keys():
            return False
        if not word and trie:
            return trie.get('end') == True

        char = word[0]
        found = False
        if char == '.':
            for key in trie.keys():
                if key == 'end':
                    continue
                found = self._search(word[1:], trie.get(key))
                if found:
                    return True
            return False
        elif char in trie:
            return self._search(word[1:], trie.get(char))
        else:
            return False

    def search(self, word: str) -> bool:
        trie = self.trie
        return self._search(word, trie)
```