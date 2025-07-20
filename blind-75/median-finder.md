# Median finder

## Explanation - self built appoach
1. Whenever adding an element, push it to the array but traversing the array and finding the insert positoin
2. When get median is called, return the median based on the size of the array

## Code - unoptimized solution
```python
class MedianFinder:
    def __init__(self):
        self.nums = []

    def addNum(self, num: int) -> None:
        idx = -1
        for i in range(len(self.nums)):
            if num <= self.nums[i]:
                idx = i
                break
        
        if idx == -1:
            idx = len(self.nums)
        self.nums.insert(idx, num)

    def findMedian(self) -> float:
        if len(self.nums) == 1:
            return self.nums[0]
        if len(self.nums) == 2:
            return sum(self.nums) / 2
        if len(self.nums) % 2 == 0:
            idx1 = len(self.nums)//2
            idx2 = idx1-1
            return (self.nums[idx1]+self.nums[idx2])/2
        else:
            return self.nums[(len(self.nums)//2)]
```

## Explanation - Optimized solution

The intuition behind this is breaking down the array in two parts, one that keeps the track of the left side and right side
i.e The one which is min heap and one which is max heap
You have the return the max from the min heap and min from the max heap if the size is even
You have to return the max from the min heap if the min heap > max_heap and min of max_heap of size of max_heap is greater than min_heap

1. Start by pushing elements to the left side
2. If left and right are not empty and the largest element from the left is greater than the smallest from the right then
    -> move that element to the right array
3. After the previous operation is done, it's okay if the difference between the size of the new two arrays (left and right) is 1
4. If the different is greater than based on whichever has the diff more than two move the element to the another array

## Code for the optimized solution
```python
class MedianFinder:

    def __init__(self):
        self.right_set = []
        self.left_set = []

    def addNum(self, num: int) -> None:
        heapq.heappush(self.left_set, -num)
        # if the largest from the left arr is greater than the smallest from the right, move that element to the right
        if self.right_set and self.left_set and -self.left_set[0] > self.right_set[0]:
            popped = -heapq.heappop(self.left_set)
            heapq.heappush(self.right_set, popped)
        
        # if the size of right set is greater by more than 1 move that to the left
        if len(self.right_set) > len(self.left_set) + 1:
            popped = heapq.heappop(self.right_set)
            heapq.heappush(self.left_set, -popped)
        
        # If the size of the right is greatrr than left than 1 move than element to the left
        if len(self.left_set) > len(self.right_set) + 1:
            popped = heapq.heappop(self.left_set)
            heapq.heappush(self.right_set, -popped)

    def findMedian(self) -> float:
        if len(self.right_set) == len(self.left_set):
            max_from_left = self.left_set[0] * -1
            min_from_right = self.right_set[0]
            return (max_from_left + min_from_right) / 2
        else:
            # if the left is largeer than return the last element from the left
            if len(self.left_set) > len(self.right_set):
                return -self.left_set[0]
            # This means that the right is larger, so return the first element from the right
            else:
                return self.right_set[0]
        
```