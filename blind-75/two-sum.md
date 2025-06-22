# two sum

### Explanation

- We will create a mapping to store each number and its index as we iterate through the array
- For each number, we calculate what the complement number should be (target - current number)
- We check if this complement exists in our mapping and ensure it's not the same index as the current number
- If we find a valid complement, we return the indices of both numbers

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        mapping = {}

        for index, num in enumerate(nums):
            mapping[num] = index
        
        for index, num in enumerate(nums):
            element_to_find = target - num
            if element_to_find in mapping and mapping[element_to_find] != index:
                return [index, mapping[element_to_find]]
```