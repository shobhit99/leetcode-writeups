# Reverse Linked List

## Explanation
1. the last element of the linked list after it's reversed is going to be None.
2. So set the first element i.e prev element to None
3. Start the loop and get the next element (next_element)
4. Set the next node of current element to prev
5. set the previous to current node
6. set the current node to next (next_element)
7. Return the prev element which is now a root node for the reversed list


```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        node = head
        prev = None

        while node != None:
            next_node = node.next
            node.next = prev
            prev = node
            node = next_node

        return prev
```























