# Lowest common ancestor

> There are two solutions, the one that i have implemented and the actual optimised solution

### Intuition behind optimized solution

1. If we start traversing the root node and if both nodes are on left and right of the current node that means the split has happened and the current node is the common ancestor
2. What we are doing to do is cover the invert cases and put the above case in else
3.  Case 1: If the p is on left and q is on left then go to left
    Case 2: If the p is on right and q is on right then go to right
    Else: It means that p and q are on left and right. i.e split

## Optimised solution code
```python
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        curr = root

        while curr:
            if p.val < curr.val and q.val < curr.val:
                curr = curr.left
            elif p.val > curr.val and q.val > curr.val:
                curr = curr.right
            else:
                return curr
```

## Explanation for my code
1. We are going to traverse the tree in post order traversal order, i.e if i am at some root then i know i have visited all the descendents (nodes below that)
2. I keep the list of nodes i have visited at that point (node) and also append the current node in that list (since current node can be ancestor of itself)
3. If the p and q are part of the list that means the current node is the common ancestor

## My code
```python

class Solution:
    def traverse(self, node):
        if not node or self.found:
            return []

        arr = []
        left_output = self.traverse(node.left)
        right_output = self.traverse(node.right)

        arr.append(node.val)
        arr.extend(left_output)
        arr.extend(right_output)

        if self.p in arr and self.q in arr and not self.found:
            self.found = True
            self.result = node

        return arr

        
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        self.found = False
        self.result = None
        self.p = p.val
        self.q = q.val

        self.traverse(root)
        
        return self.result
```