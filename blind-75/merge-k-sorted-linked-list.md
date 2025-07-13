# Merge K sorted linked list


```python
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        self.head_node = None
        self.main_node = None
        node1 = list1
        node2 = list2

        def append_to_head(node):
            if not self.head_node:
                self.head_node = node
                self.main_node = self.head_node
            else:
                self.head_node.next = node
                self.head_node = node

        while node1 or node2:
            if node1 and node2:
                if node1.val <= node2.val:
                    append_to_head(node1)
                    node1 = node1.next
                else:
                    append_to_head(node2)
                    node2 = node2.next
            elif node1:
                append_to_head(node1)
                node1 = node1.next
            elif node2:
                append_to_head(node2)
                node2 = node2.next
        
        return self.main_node
```