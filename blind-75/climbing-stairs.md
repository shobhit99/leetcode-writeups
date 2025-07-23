# Climbing stairs

## Explanation

This is just a version of fibonacii
Don't forget to memoise

## Code

```python
class Solution:
    def __init__(self):
        self.memo = {}
    def climbStairs(self, n: int) -> int:
        if n in self.memo:
            return self.memo[n]
        if n == 1:
            return 1
        if n == 2:
            return 2
        if n == 3:
            return 3
        
        op = self.climbStairs(n-2) + self.climbStairs(n-1)
        self.memo[n] = op
        return op
```