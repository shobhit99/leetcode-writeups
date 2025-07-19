# Merge K sorted List

## Explanation
> So basically you are given list of linked lists and return the sroted linked list by combining all

To solve this we can make use of the heapq
1. Just lay out all the element from all the linked list
2. Push them into the heapq
3. create new linked list out of the heap list

```python
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        flat_list = []
        for li in lists:
            node = li
            while node != None:
                flat_list.append(node.val)
                node = node.next

        hq = []
        
        for val in flat_list:
            heapq.heappush(hq, val)
        
        node = None
        head = None

        while hq:
            if not node:
                node = ListNode(heapq.heappop(hq))
                head = node
            else:
                node.next = ListNode(heapq.heappop(hq))
                node = node.next
        
        return head
```