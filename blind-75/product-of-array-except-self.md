# Product of array except self

### Explanation
- You will create an prefix array where
    - For each element from the left, keep multiying from the last element and write the that index
- you will now do same thing but from the right side
    - For each element from the right, curreent index value will be the product of the right side

- Now for the solution, at any given index the value will be. Product of index-1 * product of index+1.
    - If there's nothing at left. then just the product of index+1
    - If there's notthing at right. then just the product of index-1


### Code
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        prefix = []

        for i in range(len(nums)):
            if i == 0:
                prefix.append(nums[i])
            else:
                prefix.append(prefix[i-1] * nums[i])
        
        suffix = []
        for i in range(len(nums)-1, -1, -1):
            if i == len(nums)-1:
                suffix.append(nums[i])
            else:
                suffix.append(suffix[i-1] * nums[i])
        
        suffix = suffix[::-1]

        output = [1] * len(nums)

        for i in range(len(nums)):
            output[i] = prefix[i-1] if i > 0 else 1 * suffix[i+1] if suffix < len(nums) else 1
        
        return output
```