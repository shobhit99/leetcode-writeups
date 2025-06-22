# Longest consecutive

### Explanation
This is a bit tricky to get
- What we will do if first all we need to remove the duplicates.
- We will create the set of original nums

> The intuition behind this is that, for any num we will ignore if it has any previous elment i.e that num - 1. if it exists then we will continue. and if it doesn't that means it's starting of some sequence. 

#### So the main idea is to start counting forward for any number that might be the starting of the sequence

- For each number we will start with count as 0 and will keep incrementing until the number + 1 is not in the original set
- After each iteration of the number in the original loop. we will update the max count


### Code
```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        
        nums_set = set(nums)
        max_count = 0
        for num in nums_set:
            current_num = num
            if current_num - 1 in nums_set:
                continue
            
            count = 0
            while current_num in nums_set:
                count += 1
                current_num += 1
            max_count = max(max_count, count)
        
        return max_count
```