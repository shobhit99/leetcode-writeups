# Course schedule

## Explanation

It's a pure topological sort algorithm

1. First arrage the node in a graph format i.e course: [preq1, preq2]
2. Run the toplogical sort
3. Return if the toplogical order length is equal to the number of courses


## Code
```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        
        graph = {}

        for preq in prerequisites:
            course, pre = preq
            if course not in graph:
                graph[course] = [pre]
            else:
                graph[course].append(pre)
            
        indegree = {i: 0 for i in range(numCourses)}

        for course in graph:
            for preq in graph[course]:
                indegree[preq] += 1
        
        q = [course for course in indegree if indegree[course] == 0]

        topological_order = []
        while q:

            current = q.pop(0)
            topological_order.append(current)

            for neighbor in graph.get(current, []):
                indegree[neighbor] -=1
                if indegree[neighbor] == 0:
                    q.append(neighbor)
        
        return len(topological_order) == numCourses
```