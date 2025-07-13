# 3 Sum

## Explanation
1. Sort the entire array first
2. You will iterate all the elements and find the other two elements that equals to 0, so we will iterate until num len - 2
3. now the second and the third element will be the immediate next and the last element in the array
4. If the sum of these 3 is lower than 0, means we need to increase the left side (mind it's sorted in asc, hence from left)
5. If it's greater it means we need one smaller number, hence decrement right
6. repeat this


## Code
```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        triplets = set()

        for i in range(len(nums)-2):
            first = nums[i]
            left = i + 1
            right = len(nums)-1
            while left < right:
                second = nums[left]
                third = nums[right]
                _sum = (first + second + third)
                if _sum == 0:
                    triplets.add((first, second, third))
                    left += 1
                elif _sum > 0:
                    right -= 1
                else:
                    left += 1
        return list(triplets)
```