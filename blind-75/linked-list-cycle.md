# Linked list cycle

## Explanation
1. We make two nodes run at the same time
2. The first increments by 1
3. The second node increments by 2
4. If at any point they meet again, it means there is a cycle.
5. If at any point we encounter None, it means there is no cycle.

## Code

```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        
        if not head:
            return False

        a = head
        b = head

        while True:
            a = a.next
            b = b.next
            if b:
                b = b.next
            if not a or not b:
                return False
            if a == b:
                return True
```