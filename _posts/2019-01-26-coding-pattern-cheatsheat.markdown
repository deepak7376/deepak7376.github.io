---
layout: post
title:  "Coding Patterns Cheatsheet"
date:   2019-01-26 00:04:58 +0530
categories: dsa
summary: Coding Patterns Cheatsheet.
---

---

## Coding Patterns Cheatsheet

### Two Pointers: one input, opposite ends
Used for problems involving pairs in an array or linked list.

```python
def fn(arr):
  left = ans = 0
  right = len(arr) -1

  while left < right:
    # some logic
    if CONDITION:
      left += 1
    else:
      right -= 1
  return ans

```

### Two Pointers: two inputs, exhaust both
Used for problems involving pairs in an array or linked list.

```python
def fn(arr1, arr2):
  i = j = ans = 0

  while i < len(arr1) and j < len(arr2):
    # some logic
    if CONDITION:
      i += 1
    else:
      j += 1
  return ans


  while i < len(arr1):
    # Do logic
    i += 1
  while j < len(arr2):
    j += 1
  return ans
```

**Example Problem**: Find two numbers in a sorted array that add up to a target sum.

```python
def two_sum(nums, target):
    left, right = 0, len(nums) - 1
    while left < right:
        current_sum = nums[left] + nums[right]
        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    return []

nums = [1, 2, 3, 4, 6]
target = 6
print(two_sum(nums, target))  # Output: [1, 3]
```

### Sliding Window
Used for problems involving a contiguous subarray.

```python
def fn(arr):
    left = ans = curr = 0

    for right in range(len(arr)):
        # do logic here to add arr[right] to curr

        while WINDOW_CONDITION_BROKEN:
            # remove arr[left] from curr
            left += 1

        # update ans

    return ans
```
**Example Problem**: Find the maximum sum of a subarray of size `k`.

```python
def max_sum_subarray(arr, k):
  left = ans = curr = 0

  for right in range(len(arr)):
    curr += arr[right]

    if right - left + 1 > k:
      curr -= arr[left]
      left += 1

    if right - left + 1 == k:
      ans = max(ans, curr)

  return ans


nums = [2, 1, 5, 1, 3, 2]
k = 3
print(max_sum_subarray(nums, k))  # Output: 9
```

### Fast and Slow Pointers
Used for problems involving cycles in linked lists or arrays.

**Example Problem**: Detect a cycle in a linked list.

```python
class ListNode:
    def __init__(self, value=0, next=None):
        self.value = value
        self.next = next

def has_cycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False

# Creating a cycle for testing
node1 = ListNode(1)
node2 = ListNode(2)
node3 = ListNode(3)
node4 = ListNode(4)
node1.next = node2
node2.next = node3
node3.next = node4
node4.next = node2

print(has_cycle(node1))  # Output: True
```
### Reversing a linked list

```python
def fn(head):
    curr = head
    prev = None
    while curr:
        next_node = curr.next
        curr.next = prev
        prev = curr
        curr = next_node 
        
    return prev
```
### In-place Reversal of a Linked List
Used for problems involving reversing the nodes of a linked list in place.

**Example Problem**: Reverse a linked list.

```python
def reverse_list(head):
    prev = None
    while head:
        next_node = head.next
        head.next = prev
        prev = head
        head = next_node
    return prev

# Creating a linked list for testing
node1 = ListNode(1)
node2 = ListNode(2)
node3 = ListNode(3)
node4 = ListNode(4)
node1.next = node2
node2.next = node3
node3.next = node4

reversed_head = reverse_list(node1)
while reversed_head:
    print(reversed_head.value, end=" ")
    reversed_head = reversed_head.next  # Output: 4 3 2 1
```

### Find top k elements with heap

```python
import heapq

def fn(arr, k):
    heap = []
    for num in arr:
        # do some logic to push onto heap according to problem's criteria
        heapq.heappush(heap, (CRITERIA, num))
        if len(heap) > k:
            heapq.heappop(heap)

    return [num for num in heap]
```
**Example Problems**: 
```python
import heapq
from collections import Counter

# 1. Finding the K Smallest Elements
def k_smallest_elements(arr, k):
    heap = []
    for num in arr:
        heapq.heappush(heap, -num)
        if len(heap) > k:
            heapq.heappop(heap)

    return heap


# 2. Finding the K Most Frequent Elements
def k_most_frequent_elements(arr, k):
    counter = Counter(arr)
    heap = []
    for num, freq in counter.items():
        heapq.heappush(heap, (freq, num))
        if len(heap) > k:
            heapq.heappop(heap)

    return [num for _, num in heap]
```

### Build a prefix sum

```python
def fn(arr):
    prefix = [arr[0]]
    for i in range(1, len(arr)):
        prefix.append(prefix[-1] + arr[i])
    
    return prefix
```
### Merge Intervals
Used for problems involving overlapping intervals.

**Example Problem**: Merge overlapping intervals.

```python
def merge_intervals(intervals):
    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]
    for current in intervals[1:]:
        last = merged[-1]
        if current[0] <= last[1]:
            last[1] = max(last[1], current[1])
        else:
            merged.append(current)
    return merged

intervals = [[1, 3], [2, 6], [8, 10], [15, 18]]
print(merge_intervals(intervals))  # Output: [[1, 6], [8, 10], [15, 18]]
```
### Find number os subarray that fit exact criteria

```python
from collections import defaultdict

def fn(arr, k):
    counts = defaultdict(int)
    counts[0] = 1
    ans = curr = 0

    for num in arr:
        # do logic to change curr
        ans += counts[curr - k]
        counts[curr] += 1
    
    return ans
```
### Monotonic increasing stack

```python
def fn(arr):
    stack = []
    ans = 0

    for num in arr:
        # for monotonic decreasing, just flip the > to <
        while stack and stack[-1] > num:
            # do logic
            stack.pop()
        stack.append(num)
    
    return ans
```
### Cyclic Sort
Used for problems involving numbers in a given range.

**Example Problem**: Find the missing number in an array containing `n` distinct numbers taken from 0 to `n`.

```python
def find_missing_number(nums):
    i, n = 0, len(nums)
    while i < n:
        j = nums[i]
        if j < n and nums[i] != nums[j]:
            nums[i], nums[j] = nums[j], nums[i]
        else:
            i += 1
    for i in range(n):
        if nums[i] != i:
            return i
    return n

nums = [4, 0, 3, 1]
print(find_missing_number(nums))  # Output: 2
```
---
## Tree
### 7. Tree Traversal
Used for problems involving tree traversals.

**Example Problem**: Perform in-order traversal of a binary tree.

```python
class TreeNode:
    def __init__(self, value=0, left=None, right=None):
        self.value = value
        self.left = left
        self.right = right

def inorder_traversal(root):
    result = []
    def traverse(node):
        if not node:
            return
        traverse(node.left)
        result.append(node.value)
        traverse(node.right)
    traverse(root)
    return result

# Creating a binary tree for testing
root = TreeNode(1)
root.right = TreeNode(2)
root.right.left = TreeNode(3)

print(inorder_traversal(root))  # Output: [1, 3, 2]
```
### Binary Tree: DFS (recursive)

```python
def dfs(root):
    if not root:
        return
    
    ans = 0

    # do logic
    dfs(root.left)
    dfs(root.right)
    return ans
```
### Binary Tree: DFS (iterative)
```python
def dfs(root):
    stack = [root]
    ans = 0

    while stack:
        node = stack.pop()
        # do logic
        if node.left:
            stack.append(node.left)
        if node.right:
            stack.append(node.right)

    return ans
```

### Binary Tree: BFS

```python
from collections import deque

def fn(root):
    queue = deque([root])
    ans = 0

    while queue:
        current_length = len(queue)
        # do logic for current level

        for _ in range(current_length):
            node = queue.popleft()
            # do logic
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)

    return ans
```

---
## Graph

### Graph: DFS (recursive)

```python
def fn(graph):
    def dfs(node):
        ans = 0
        # do some logic
        for neighbor in graph[node]:
            if neighbor not in seen:
                seen.add(neighbor)
                ans += dfs(neighbor)
        
        return ans

    seen = {START_NODE}
    return dfs(START_NODE)
```

### Graph: DFS (iterative)

```python
def fn(graph):
    stack = [START_NODE]
    seen = {START_NODE}
    ans = 0

    while stack:
        node = stack.pop()
        # do some logic
        for neighbor in graph[node]:
            if neighbor not in seen:
                seen.add(neighbor)
                stack.append(neighbor)
    
    return ans
```
### Subsets
Used for problems involving subsets of a set.

**Example Problem**: Generate all subsets of a given set.

```python
def subsets(nums):
    result = []
    def backtrack(start, current):
        result.append(list(current))
        for i in range(start, len(nums)):
            current.append(nums[i])
            backtrack(i + 1, current)
            current.pop()
    backtrack(0, [])
    return result

nums = [1, 2, 3]
print(subsets(nums))  # Output: [[], [1], [1, 2], [1, 2, 3], [1, 3], [2], [2, 3], [3]]
```

### Topological Sort
Used for problems involving directed acyclic graphs (DAGs).

**Example Problem**: Find a topological ordering of a given graph.

```python
from collections import defaultdict, deque

def topological_sort(vertices, edges):
    graph = defaultdict(list)
    in_degree = {i: 0 for i in range(vertices)}
    for u, v in edges:
        graph[u].append(v)
        in_degree[v] += 1
    queue = deque([k for k in in_degree if in_degree[k] == 0])
    sorted_order = []
    while queue:
        vertex = queue.popleft()
        sorted_order.append(vertex)
        for neighbor in graph[vertex]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
    return sorted_order if len(sorted_order) == vertices else []

vertices = 6
edges = [(5, 2), (5, 0), (4, 0), (4, 1), (2, 3), (3, 1)]
print(topological_sort(vertices, edges))  # Output: [4, 5, 2, 0, 3, 1]
```

### Dynamic Programming
Used for problems involving overlapping subproblems and optimal substructure.

**Example Problem**: Find the length of the longest increasing subsequence.

```python
def length_of_lis(nums):
    if not nums:
        return 0
    dp = [1] * len(nums)
    for i in range(len(nums)):
        for j in range(i):
            if nums[i] > nums[j]:
                dp[i] = max(dp[i], dp[j] + 1)
    return max(dp)

nums = [10, 9, 2, 5, 3, 7, 101, 18]
print(length_of_lis(nums))  # Output: 4 (2, 3, 7, 101)
```
