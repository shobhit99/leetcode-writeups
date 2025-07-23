# House Robber

## Explanation
1. Start with the index 0
2. At any point you can consider current and output of `func(current+2)` OR current+1 and `func(current+3)`
3. Handle the edge cases for the last 3 homes
4. memoise the index for optimisation

## Code
```python
class Solution:
    def __init__(self):
        self.memo = {}

    def traverse(self, index):
        if index in self.memo:
            return self.memo[index]
        if index >= len(self.nums):
            return 0
        if index == len(self.nums) - 1:
            return self.nums[index]
        if index == len(self.nums) - 2:
            return max(self.nums[index], self.nums[index+1])
        
        op = max(
            self.nums[index] + self.traverse(index+2),
            self.nums[index+1] + self.traverse(index+3)
        )
        if index not in self.memo:
            self.memo[index] = op
        return op


    def rob(self, nums: List[int]) -> int:
        self.nums = nums

        output = self.traverse(0)

        return output
```