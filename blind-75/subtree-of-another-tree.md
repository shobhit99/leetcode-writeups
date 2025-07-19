# Subtree of another tree

## Explanation

1. Traverse the tree
2. On each node of the first tree. call the function with params as that node and the subtree node
3. Check if both are same by using the same tree algorithm
4. If they are same then update the global var is same

```python
class Solution:
    def is_same_tree(self, node1, node2):

        if node1 and not node2:
            return False
        if node2 and not node1:
            return False
        
        if not node1 and not node2:
            return True
        
        if node1.val != node2.val:
            return False
        op1 = self.is_same_tree(node1.left, node2.left)
        op2 = self.is_same_tree(node1.right, node2.right)
        
        if op1 and op2:
            return True
        return False


    def traverse(self, node):
        if self.is_same:
            return

        if not node:
            return
        
        is_same = self.is_same_tree(node, self.subRoot)
        if is_same:
            self.is_same = True
            return

        self.traverse(node.left)
        self.traverse(node.right)

    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        self.subRoot = subRoot
        self.root = root

        self.is_same = False

        self.traverse(root)


        return self.is_same
```