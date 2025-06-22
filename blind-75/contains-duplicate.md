# contains-duplicate

### Explanation
Iterate the array and keep the track of numbers. if any number is previously seen. then return True

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        num_mapping = {}

        for num in nums:
            if num not in num_mapping:
                num_mapping[num] = True
            else:
                return True
        
        return False
```
