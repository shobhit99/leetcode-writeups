# Combination Sum

## Explanation

This is a slight modification of the powerset / supsert.
You don't need to jump to the next index, instead keep recurring with the same index until the sum of arr becomes more than target
And once that happens, return and increment the index and do the same thing again

## Code
```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        self.result = []
        
        def recur(sub_arr, index):
            if index >= len(candidates) or sum(sub_arr) >= target:
                if sum(sub_arr) == target:
                    self.result.append(sub_arr[::])
                return
            
            sub_arr.append(candidates[index])
            recur(sub_arr, index)
            sub_arr.pop()
            recur(sub_arr, index+1)
        
        recur([], 0)
        return self.result
```