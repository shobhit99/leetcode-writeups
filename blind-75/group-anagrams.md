
# Group anagrams

## Explanation

- we that the characters in the word are from a-z
- So there are 26 distinct characters in any given word
- For any anagram to be equal to any other anagram, the count of each a-z arranged sequentially should match
- we will create a dictionary with the key as [0] * 26 i.e 0 for each character
- if there's another word with same character occurrences then it will fall under same key
- we will similary group them and return the answer


### Solution

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        visited_words = {}

        for word in strs:
            arr = [0] * 26

            for letter in word:
                arr[ord(letter) % 97] = arr[ord(letter) % 97] + 1
            
            tuple_key = tuple(arr)
            if not tuple_key in visited_words:
                visited_words[tuple(arr)] = [word]
            else:
                visited_words[tuple(arr)].append(word)
        
        return list(visited_words.values())
```