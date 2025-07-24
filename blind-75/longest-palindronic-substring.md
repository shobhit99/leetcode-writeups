# Longest palindromic substring

## Explanation
1. Iterate the string
2. In each iteration, start with l and r as same and expand words until s[l] and s[r] are same and update the longest
3. Do same, but this time start l with i-1, this is to cover the case where the palindormic string might be even
4. return the longest string

## Code
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        
        longest = ""
        s_len = len(s)

        for i in range(s_len):
            l = r = i
            while l >= 0 and r < s_len and s[l] == s[r]:
                if r - l + 1 > len(longest):
                    longest = s[l:r+1]
                l -= 1
                r += 1
            
            l = i - 1
            r = i
            while l >= 0 and r < s_len and s[l] == s[r]:
                if r - l + 1 > len(longest):
                    longest = s[l:r+1]
                l -= 1
                r += 1
            
        return longest
```