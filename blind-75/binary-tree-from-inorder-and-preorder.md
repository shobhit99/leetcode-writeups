# Binary tree from inorder and preorder

## Explanation

Just memorize this code ffs


```python
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        
        if not inorder:
            return None
        
        p = preorder.pop(0)
        node = TreeNode(p)
        node.left = self.buildTree(preorder, inorder[:inorder.index(p)])
        node.right = self.buildTree(preorder, inorder[inorder.index(p)+1:])

        return node
```