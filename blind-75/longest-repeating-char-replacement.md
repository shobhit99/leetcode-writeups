# Longest repeating character replacement

## Explanation

1. We will maintain
    a. current window
    b. occurrence for each character in the window
    c. current max length
    d. max occuring character
2. For each iteartion we will
    a. increment the right
    b. see if the occurrences of the right char > max_char
        if yes then, max_char = right_char
    c. see if the window - max_char <= k
    d. if yes then update the max_len
    e. else slide the window

## Code
```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        s = s.upper()
        left = right = 0
        max_char = s[left].upper()
        max_len = 1

        char_mapping = {x:0 for x in string.ascii_uppercase}

        while right < len(s):
            window_size = right + 1 - left
            char_mapping[s[right]] += 1

            if char_mapping[s[right]] >= char_mapping[max_char]:
                max_char = s[right]
            
            if window_size - char_mapping[max_char] <= k:
                max_len = max(max_len, window_size)
            else:
                # slide the window
                char_mapping[s[left]] -= 1
                left += 1
            
            right += 1
        
        return max_len
```