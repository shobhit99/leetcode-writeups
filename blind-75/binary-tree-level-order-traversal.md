# Binary tree level order traversal

## Explanation
Just run the BFS algo and store the each level in the array and keep appending to the main array

## Code
```python
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        orders = []
        q = []
        q.append(root)
        while q:
            current_level = []
            q_len = len(q)
            for i in range(q_len):
                node = q.pop(0)
                current_level.append(node.val)
                if node.left:
                    q.append(node.left)
                if node.right:
                    q.append(node.right)
            orders.append(current_level)
        
        return orders
```