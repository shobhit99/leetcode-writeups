# Find min in rotated sorted array

## Explanation

1. Start with l = 0 and r = last element
2. while l < r we will
3. See if element in right is less than element in the mid. that means the min is in the right part
4. In that case we will shift the left to mid + 1
5. else it means that the min is in the left
6. In that case we will shift the r to mid. (because the r could be the min / only element)

## Code
```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        l = 0
        r = len(nums) - 1

        while l < r:
            mid = (l+r)//2
            if nums[r] < nums[mid]:
                l = mid + 1
            else:
                r = mid
        

        return nums[l]
```