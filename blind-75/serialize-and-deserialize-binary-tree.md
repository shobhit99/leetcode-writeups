# Serialize and deserialize binary tree

## Explanation

Just convert the tree to json and then return the stringified json
Deserialize it again by converting json into the tree

## Code
```python
class Codec:

    def _serialize(self, node):
        if not node:
                    return None
        element = {
            'val': node.val,
            'left': self._serialize(node.left),
            'right': self._serialize(node.right)
        }

        return element

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """

        return json.dumps(self._serialize(root))
        
    def _deserialize(self, data):
        if not data:
            return None
        node = TreeNode(data['val'])
        node.left = self._deserialize(data['left'])
        node.right = self._deserialize(data['right'])

        return node

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        op = self._deserialize(json.loads(data))
        return op
```