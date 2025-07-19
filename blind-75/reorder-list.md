# Reorder list

## Explanation

> The expected solution goes like this

Given an input 1->2->3->4->5
1. You will first find the mid of the linked list i.e 3
2. Now create two linked lists
    a. First Linked List -> Iterates till the mid (1->2->3)
    b. Second Linked List -> Iterates from the last to mid - (5->4)
3. Now join these lists by alternatively picking the element from each one, starting with the first list
4. So we have 1->5->2->4->3

> The code is different and not the above logic
```python
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        arr = []

        node = head
        while node != None:
            arr.append(node)
            node = node.next
        
        l = 0
        r = len(arr) - 1

        node = arr[0]
        x = True

        for i in range(len(arr)):
            if x:
                node.next = arr[r]
                node = node.next
                l += 1
            else:
                node.next = arr[l]
                node = node.next
                r -= 1
            x = not x
        
        node.next = None
```