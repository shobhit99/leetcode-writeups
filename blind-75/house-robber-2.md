# House Robber 2

## Explanation

This is just a variation of the house robber
1. The trick is
    - If it's a cirle, that means, if you have robbed first then you can't rob last
    - And if you rob second, means you can rob last
2. What we will do is remove the first element and rob and save the output in output1
3. Now, we will remove the last element and start robbing from first house and save the output in output2
4. Return max of both outputs

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
        if len(nums) == 1:
            return nums[0]

        self.nums = nums[1:]
        self.memo = {}
        output1 = self.traverse(0)

        self.memo = {}
        self.nums = nums[:-1]
        output2 = self.traverse(0)

        return max(output1, output2)
```