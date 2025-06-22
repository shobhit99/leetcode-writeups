# Valid Palindrome

### Explanation

- we first created a new string by ignoring anything other than alphabet and number
- then we checked if the new string is palindrome or not


### Code
```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        new_str = ""

        for char in s:
            char = char.lower()
            if char not in [*string.ascii_lowercase, *'0987654321']:
                continue
            new_str += char

        i = 0
        j = len(new_str) - 1
        while i < j:
            if new_str[i] != new_str[j]:
                return False
            i += 1
            j -= 1
        return True
```