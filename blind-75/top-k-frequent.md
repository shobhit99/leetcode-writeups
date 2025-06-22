# Top K frequent

### Explanation

- We will first map the occurrence of each element with it's occurrence count
- We will then get the unique set of occurrences i.e values of all the mappings
- now we will create new map and for each count we will keep the list of values in the original map which occcurred that many times
- finally we will iterate the unique counts in descending order and add the values to the output for the first k elements

### Code
```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        occ = {}
        target = k

        for n in nums:
            occ[n] = occ.get(n, 0) + 1
        
        counts = sorted(set(occ.values()), reverse=True)

        count_n_mapping = {}
        for k, v in occ.items():
            if v not in count_n_mapping:
                count_n_mapping[v] = [k]
            else:
                count_n_mapping[v].append(k)

        output = []
        n = target
        for c in counts:
            values = count_n_mapping[c]
            if n == 0:
                break
            if len(values) <= n:
                n -= len(values)
                output.extend(values)
            else:
                output.extend(values[:n])
                n -= len(values[:n])
                break
        
        return output
```