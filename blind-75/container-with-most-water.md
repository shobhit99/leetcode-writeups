# Container with most water

### Explanation

1. We start with left and right pointer as 0 and len of heights - 1
2. We can only fit the water of the lower height, since anything higher will overflow
3. We will calculate the total water between right and left and set the max
4. we will then shift the the smaller height to left / right, because we want to maximize the water

### Code

```
class Solution:
    def maxArea(self, height: List[int]) -> int:
        l = 0
        r = len(height) - 1

        maximum = 0
        while l <= r:
            total_weight = (r-l) * min(height[l], height[r])
            maximum = max(total_weight, maximum)
            if height[l] <= height[r]:
                l += 1
            else:
                r -= 1
        
        return maximum
```