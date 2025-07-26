# Alien Dictionary

## Understanding the problem.
In any english dictionary, the words are ordered based on the alphabet. we know that the ordering goes from a, b, c ... till z. and entire dictionary is strucutred around this rule

But in the alien diciontary this ordering is not same as our standard ordering i.e a->z, it could be anything e.g e,x,y. we are given the set of words that obey this order. and we need to return the ordering of known alphabets in this dictionary based on the given words

The given words might have incorrect ordering. e.g apple, ball, applet. since word applet is in wrong position, we should return empty string

## Explanation
Consider the sample input
["wrt","wrf","er","ett","rftt"]

If we write it down
w r t
w r f
e r
e t t
r f t t t

We can find the set rules based on the previous characters of two words. e.g
abc
abd
says that d comes after c since ab part is same in the above words

We will compare, 2 words at a time, and identify the link
- First Occurrence
w r t
w r f

here part w r is same, so it means that f comes after t

1. Start loop on words until len(words)-1 (as we are comparing two words at a time)
2. for these two words, get the len of the smallest among two, as we are going to iterate these two words simultaneously
3. if the curr_word[i] != curr_word[j] -> This means we got a link we can add to the graph for adjacency list
4. Once we have all the links, we will run topological sort on the graph created
5. If there's a cycle means the words are in invalid ordering, else return the topological ordering

> To handle one edge case in the initial for loop, if the curr[:min_len_word_len] == next[:min_len_word_len] and the current word is greater than next word. This is an invalid case. we return "" directly from here. e.g ["abc", "ab"]


## Code
```python
from collections import OrderedDict, deque

class Solution:
    def getGraph(self, links):
        indegree = {}
        graph = {}

        for node in links:
            if node not in indegree:
                indegree[node] = 0
            for neighbor in links[node]:
                if neighbor not in indegree:
                    indegree[neighbor] = 0

        for node in links:
            for neighbor in links[node]:
                if node not in graph:
                    graph[node] = set(neighbor)
                    indegree[neighbor] += 1
                else:
                    graph[node].add(neighbor)
                    indegree[neighbor] += 1
        
        return indegree, graph

    def topological_sort(self, indegree, graph):
        queue = deque([x for x in indegree if indegree[x] == 0])
        toplogical_order = []

        while queue:
            node = queue.popleft()
            toplogical_order.append(node)

            for neighbor in graph.get(node, {}):
                indegree[neighbor] -= 1
                if indegree[neighbor] == 0:
                    queue.append(neighbor)
        
        if len(toplogical_order) != len(indegree):
            return ""
        return ''.join(toplogical_order)

    def alienOrder(self, words):
        links = {x: set() for w in words for x in w}  
        for i in range(len(words)-1):
            current_word, next_word = words[i], words[i+1]

            min_len = min(len(current_word), len(next_word))

            if len(current_word) > len(next_word) and current_word[:min_len] == next_word[:min_len]:
                return ""
            j = 0
            for j in range(min_len):
                if current_word[j] != next_word[j]:
                    links[current_word[j]].add(next_word[j])
                    break
        
        indegree, graph = self.getGraph(links)
        order = self.topological_sort(indegree, graph)
        return order
```