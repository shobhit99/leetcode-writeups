# Is Anagram

### Explanation

- We will first create a mapping with occurrence for each character
- We will iterate the target string and deduct 1 for each occurrence of that char in target string
    - If any char is not present in source mapping, we can instantly say that it's not an angram
- In the end if all the values are exactly 0 in source mapping, we can say that it was a perfect anagram

### Code
```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        source_mapping = {}

        for char in s:
            source_mapping[char] = source_mapping.get(char, 0) + 1
        
        for char in t:
            if char in source_mapping:
                source_mapping[char] -= 1
            else:
                return False
        
        return all([x == 0 for x in source_mapping.values()])
```