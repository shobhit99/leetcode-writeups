# Min window substring

## Explanation
The main logic is
1. Start with the pointers l and r = 0
2. Check if the t exists in the current window
3. If it does then we increment the left to minimize the window and still try to find it
4. If it does then update the min
5. If it doesn't increment the right pointer

Intuitively, you will create a function to see if the t exists in the window, the main magic is to optimise this function

1. The way to do this is create a map of target
2. Whenever we include the element in the window, decrease the char from the mapping by 1
3. Whenever we exclude it by shifting left pointer then add 1 back to it

Now, the t exists in the s if all of the characters in mapping are <= 0, in other word !(atleast one char is greater than 0)

## Code

```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        left = right = 0

        a = [0] * 26
        min_window = 99999999
        result = ""

        if len(t) > len(s):
            return ""

        target_mapping = {}
        for char in t:
            target_mapping[char] = target_mapping.get(char, 0) + 1
        
        if s[left] in target_mapping:
            target_mapping[s[left]] -= 1

        while right < len(s):
            window = s[left:right+1]

            if not any([x > 0 for x in target_mapping.values()]):
                if len(window) < min_window:
                    result = window
                    min_window = len(window)
                if s[left] in target_mapping:
                    target_mapping[s[left]] += 1
                left += 1
            else:
                right += 1
                if right < len(s) and s[right] in target_mapping:
                    target_mapping[s[right]] -= 1
                
        
        return result
```