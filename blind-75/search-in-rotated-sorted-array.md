# Search in rotated sorted array

## Explanation
1. See if the left part is sorted
    a. If the element is between the left sorted part then make right as mid - 1
    b. else make left as mid + 1
2. See if the right part is sorted
    a. If the element in between mid and right then make left as mid + 1
    b. else make right as mid - 1

## Code

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l = 0
        r = len(nums) - 1

        while l <= r:
            mid = (l+r)//2
            if nums[mid] == target:
                return mid
            if nums[l] <= nums[mid]:
                if nums[l] <= target <= nums[mid]:
                    r = mid - 1
                else:
                    l = mid + 1
            elif nums[mid] <= nums[r]:
                if nums[mid] <= target <= nums[r]:
                    l = mid + 1
                else:
                    r = mid - 1
        
        return -1
```