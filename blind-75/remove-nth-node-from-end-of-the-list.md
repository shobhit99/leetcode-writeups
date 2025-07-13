# Remove nth node from the end of the list

## Explanation
1. we will first find out the lenght of the linked list
2. we will get the index of the element to be removed
3. we will iterated the LL again and join the prev node to the next node in the list if we reach that index
4. if the prev node is empty, that means we are supposed to remove the first node, in that case just return the next node as head


## Code
```python
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        length_of_the_list = 0

        node = head
        while node != None:
            length_of_the_list += 1
            node = node.next
        
        element_to_remove = length_of_the_list - n

        i = 0
        node = head
        prev = None
        while node != None:
            if element_to_remove == i:
                if prev:
                    prev.next = node.next
                else:
                    return node.next
            else:
                prev = node
                node = node.next
            i += 1
        
        return head
```