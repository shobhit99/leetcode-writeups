# Palindromic substring

## Explanation
Same appraoch as longest palindrome, just that in each iteration keep the count of the palindromes


## Code
```python
class Solution:
    def countSubstrings(self, s: str) -> int:

        if len(s) == 1:
            return 1
        
        i = 0
        count = 0

        while i < len(s):
            l = r = i
            while l >= 0 and r < len(s) and s[l] == s[r]:
                count += 1
                l -= 1
                r += 1
            i += 1

        i = 0
        while i < len(s)-1:
            l = i
            r = i + 1
            while l >= 0 and r < len(s) and s[l] == s[r]:
                count += 1
                l -= 1
                r += 1
            i += 1
    
        
        return count
```